# 08 — LangChain and RAG Applications

## Chapter purpose

This chapter turns the short idea of “use LangChain and RAG” into a full mental model for building real AI applications. By the end, you should understand not only the steps of a RAG pipeline, but also why each step exists, what can go wrong, and how to design a system that is actually useful in production.

RAG means **Retrieval-Augmented Generation**. The basic idea is simple: before asking a language model to answer, retrieve relevant information from trusted sources and give that information to the model as context.

The deeper idea is more important: RAG is a way to connect a language model to an external memory that can be updated, inspected, cited, filtered, and evaluated.

---

## 1. Why LLM frameworks exist

A simple LLM demo usually looks like this:

```text
user question -> prompt -> model -> answer
```

That is enough for a toy example. It is not enough for a real product.

A real AI application usually needs to:

1. receive a user request;
2. validate the input;
3. load previous messages or user state;
4. retrieve relevant documents;
5. format the retrieved information;
6. call a model;
7. parse the model output;
8. call tools if needed;
9. validate the final answer;
10. log what happened;
11. evaluate quality over time.

You can build all of this manually. In fact, when you are learning, building it manually once is useful. But as your apps grow, you need structure. Frameworks such as LangChain help organize common LLM application patterns: models, prompts, tools, retrieval, agents, memory, tracing, and evaluation.

### Important distinction

LangChain is not the intelligence. The model is the intelligence provider. LangChain is the orchestration layer around the model.

Think of it like this:

```text
Model       = engine
Prompt      = instruction
Retriever   = search system
Tool        = callable function
LangChain   = application wiring
Your backend = product system
```

If you do not understand this distinction, you may overuse frameworks and create complex systems that are harder to debug than a direct model call.

---

## 2. When you do not need LangChain

A common beginner mistake is to install a framework too early.

You probably do **not** need LangChain if your app only does this:

```text
Take a short user input -> call one model -> return one answer
```

Example: a button that rewrites a product description in a friendlier tone.

For that, a direct model call is simpler and easier to debug.

You may benefit from LangChain when your app needs:

- multiple model providers;
- reusable prompt templates;
- document loading and splitting;
- retrieval pipelines;
- tool calling;
- agent loops;
- tracing and debugging;
- chains of steps;
- integration with vector databases;
- evaluation workflows.

The rule is simple: use the framework when it reduces complexity, not when it adds complexity.

---

## 3. The problem RAG solves

LLMs have several limitations:

### 3.1 They do not know your private data

A model does not automatically know your company documents, university documents, customer tickets, codebase, PDFs, Notion pages, or internal policies.

### 3.2 They may be outdated

Even if a model knows general information, that knowledge may not include recent changes.

### 3.3 They can hallucinate

A model may generate an answer that sounds fluent and confident but is not supported by evidence.

### 3.4 They cannot cite internal truth unless you provide it

If you want answers based on documents, the model needs access to those documents or retrieved pieces of those documents.

RAG solves these problems by adding a retrieval step.

Instead of this:

```text
Question -> Model -> Answer
```

RAG does this:

```text
Question -> Search trusted knowledge -> Model with context -> Grounded answer
```

---

## 4. RAG as open-book exam

A useful analogy: an LLM without RAG is like a student answering from memory. Sometimes it is right, sometimes it guesses.

An LLM with RAG is like a student taking an open-book exam. The student still needs reasoning ability, but now the answer can be based on specific pages from the book.

The quality of the final answer depends on two things:

1. Did the student receive the right pages?
2. Did the student correctly use those pages?

In RAG terms:

1. Did retrieval find the right chunks?
2. Did generation use the chunks faithfully?

This is why RAG evaluation has two parts: retrieval evaluation and answer evaluation.

---

## 5. The full RAG pipeline

A complete RAG system has two phases.

### Phase A: Indexing phase

This happens before the user asks a question.

```text
Documents -> Clean -> Split -> Embed -> Store
```

Steps:

1. collect documents;
2. extract text;
3. clean the text;
4. split the text into chunks;
5. create embeddings for each chunk;
6. store embeddings plus metadata in a vector database.

### Phase B: Query phase

This happens when the user asks a question.

```text
Question -> Embed question -> Retrieve chunks -> Build prompt -> Generate answer
```

Steps:

1. receive the question;
2. optionally rewrite or classify the question;
3. embed the question;
4. retrieve similar chunks;
5. optionally rerank the chunks;
6. build a prompt with context;
7. call the model;
8. validate the answer;
9. return answer plus sources.

---

## 6. Text diagram of a RAG system

```text
                 INDEXING TIME

       ┌──────────────┐
       │  Documents   │
       └──────┬───────┘
              │
              v
       ┌──────────────┐
       │ Text extract │
       └──────┬───────┘
              │
              v
       ┌──────────────┐
       │   Chunking   │
       └──────┬───────┘
              │
              v
       ┌──────────────┐
       │  Embeddings  │
       └──────┬───────┘
              │
              v
       ┌──────────────┐
       │ Vector store │
       └──────────────┘


                  QUERY TIME

       ┌──────────────┐
       │ User question│
       └──────┬───────┘
              │
              v
       ┌──────────────┐
       │ Query embed  │
       └──────┬───────┘
              │
              v
       ┌──────────────┐
       │  Retrieve    │
       └──────┬───────┘
              │
              v
       ┌──────────────┐
       │ RAG prompt   │
       └──────┬───────┘
              │
              v
       ┌──────────────┐
       │     LLM      │
       └──────┬───────┘
              │
              v
       ┌──────────────┐
       │ Answer + refs│
       └──────────────┘
```

---

## 7. Documents are not automatically useful

Many beginners think RAG begins with embeddings. It does not. RAG begins with document quality.

Bad documents create bad retrieval. Bad retrieval creates bad answers.

Before embedding anything, ask:

- Is this document still valid?
- Is it duplicated elsewhere?
- Does it contain headers, footers, page numbers, or navigation noise?
- Is the text extraction clean?
- Are tables preserved correctly?
- Are images important?
- Is the document language consistent?
- Does each document have useful metadata?

Example: imagine a PDF about visa requirements. If the extraction loses tables, page headings, or dates, the model may answer incorrectly even if retrieval technically works.

---

## 8. Chunking explained deeply

Chunking means splitting documents into smaller pieces that can be retrieved independently.

A model cannot receive every document all the time. Even if the context window is large, sending everything is expensive and noisy. Retrieval chooses a small set of relevant chunks.

### 8.1 Bad chunking example

Suppose the original paragraph says:

```text
Students applying for a long-stay visa must submit proof of admission, proof of financial means, health insurance, and a valid passport. The passport must be valid for at least twelve months after arrival.
```

Bad chunk 1:

```text
Students applying for a long-stay visa must submit proof of admission,
```

Bad chunk 2:

```text
proof of financial means, health insurance, and a valid passport. The passport must be valid for at least twelve months after arrival.
```

The first chunk is incomplete. The second chunk lacks the subject. Retrieval may find only one and lose meaning.

### 8.2 Better chunk

```text
Students applying for a long-stay visa must submit proof of admission, proof of financial means, health insurance, and a valid passport. The passport must be valid for at least twelve months after arrival.
```

This chunk preserves the complete rule.

### 8.3 Chunk size tradeoff

Small chunks:

- easier to retrieve precisely;
- cheaper to send;
- may lose context.

Large chunks:

- preserve more context;
- may include irrelevant text;
- cost more tokens;
- may reduce retrieval precision.

A practical starting point for text documents is often a few hundred words per chunk, with overlap when needed. But there is no universal perfect size. You must evaluate with real questions.

### 8.4 Chunk overlap

Overlap means repeating a small part of the previous chunk in the next chunk. This helps when important meaning crosses boundaries.

Example:

```text
Chunk 1: ... financial means, health insurance, and a valid passport.
Chunk 2: valid passport. The passport must be valid for at least twelve months after arrival ...
```

Overlap prevents the second chunk from losing the topic.

### 8.5 Structure-aware chunking

For serious systems, split by document structure:

- headings;
- sections;
- paragraphs;
- bullet lists;
- table boundaries;
- code blocks;
- FAQ entries.

Structure-aware chunking is usually better than blind fixed-size splitting.

---

## 9. Embeddings in RAG

An embedding is a vector: a list of numbers representing meaning.

The goal is that similar meanings have similar vectors.

Example:

```text
Question: What documents do I need for a student visa?
Chunk: Students must submit proof of admission, passport, financial means, and insurance.
```

These texts do not use exactly the same words, but they are semantically related. Embeddings allow the retriever to find the chunk even without exact keyword overlap.

### 9.1 Simple mental model

Imagine every text is placed on a huge map of meaning.

Texts about student visas are near each other. Texts about neural networks are somewhere else. Texts about football predictions are somewhere else again.

A query embedding asks: “Which stored chunks are closest to this question on the meaning map?”

---

## 10. Vector database

A vector database stores embeddings and metadata so you can search by similarity.

Each record usually contains:

```json
{
  "id": "chunk_001",
  "text": "Students applying for a long-stay visa must submit...",
  "embedding": [0.12, -0.03, 0.44],
  "metadata": {
    "source": "student_visa_checklist.pdf",
    "page": 3,
    "section": "Required documents",
    "language": "en",
    "updated_at": "2026-05-26"
  }
}
```

The embedding is used for similarity search. The metadata is used for filtering, citations, and access control.

### 10.1 Why metadata matters

Without metadata, you may know the answer but not where it came from.

Good metadata lets you answer:

- Which document supports this answer?
- Which page?
- Which section?
- Is the document outdated?
- Is the user allowed to see this chunk?
- Is this chunk in the right language?

For production RAG, metadata is not optional.

---

## 11. Retrieval strategies

### 11.1 Semantic search

Semantic search uses embeddings to find meaning similarity.

Good for:

- natural-language questions;
- paraphrased information;
- messy user wording;
- conceptual search.

Weak for:

- exact IDs;
- exact dates;
- exact names;
- rare keywords.

### 11.2 Keyword search

Keyword search matches words directly.

Good for:

- names;
- IDs;
- product codes;
- legal terms;
- exact phrases.

Weak for:

- paraphrases;
- synonyms;
- questions written differently from documents.

### 11.3 Hybrid search

Hybrid search combines semantic and keyword search.

This is often stronger than either alone.

Example:

A user asks:

```text
What is the handling fee for the Belgium D visa after July 1?
```

Keyword search helps find “handling fee,” “D visa,” and “July 1.” Semantic search helps find related wording like “long-stay visa application fee.”

---

## 12. Reranking

Initial retrieval may return 20 possible chunks. A reranker scores them more carefully and chooses the best few.

Reranking is useful when:

- many chunks are similar;
- documents are long;
- precision matters;
- the first vector search is noisy;
- the final answer must cite strong evidence.

Simple pipeline:

```text
query -> retrieve top 20 -> rerank -> keep top 5 -> generate answer
```

Reranking can improve quality but adds latency and cost. Use it when the accuracy gain is worth it.

---

## 13. Building the RAG prompt

The prompt is where retrieval and generation meet.

A weak RAG prompt says:

```text
Answer this question using the context.
```

A stronger RAG prompt says:

```text
You are answering using retrieved context.
Use only the context provided.
If the context is insufficient, say that the answer is not available in the provided documents.
Cite the source id for each important claim.
Keep the answer concise and practical.

Context:
[chunk 1]
[chunk 2]
[chunk 3]

Question:
...
```

### 13.1 Why this works better

The model needs clear rules:

- what sources to use;
- what to do when information is missing;
- how to handle uncertainty;
- how to format the answer;
- how to cite evidence.

RAG is not only retrieval. It is retrieval plus instruction design.

---

## 14. A minimal RAG implementation in Python

This example is intentionally simple. It does not require a vector database. It uses a toy similarity function so you understand the flow before using real embeddings.

```python
from dataclasses import dataclass
from typing import List

@dataclass
class Chunk:
    id: str
    text: str
    source: str

chunks = [
    Chunk(
        id="visa_001",
        text="Students must submit proof of admission, financial means, health insurance, and a valid passport.",
        source="student_visa_checklist.pdf"
    ),
    Chunk(
        id="ai_001",
        text="RAG retrieves relevant document chunks and gives them to a language model as context.",
        source="ai_engineering_notes.md"
    ),
]

def simple_score(query: str, text: str) -> int:
    query_words = set(query.lower().split())
    text_words = set(text.lower().split())
    return len(query_words.intersection(text_words))

def retrieve(query: str, top_k: int = 2) -> List[Chunk]:
    scored = sorted(
        chunks,
        key=lambda chunk: simple_score(query, chunk.text),
        reverse=True,
    )
    return scored[:top_k]

def build_prompt(query: str, retrieved: List[Chunk]) -> str:
    context = "\n\n".join(
        f"Source: {chunk.source} | ID: {chunk.id}\n{chunk.text}"
        for chunk in retrieved
    )
    return f"""
Use only the context below to answer the question.
If the answer is not in the context, say that the documents do not contain enough information.

Context:
{context}

Question:
{query}
""".strip()

query = "What documents do students need for a visa?"
retrieved_chunks = retrieve(query)
prompt = build_prompt(query, retrieved_chunks)
print(prompt)
```

This is not production RAG, but it teaches the architecture:

1. store chunks;
2. retrieve relevant chunks;
3. build a grounded prompt;
4. ask a model to answer using the context.

Once you understand this, replacing `simple_score` with real embeddings becomes much easier.

---

## 15. Real RAG architecture with LangChain

A LangChain-style RAG app often includes:

- document loaders;
- text splitters;
- embedding model;
- vector store;
- retriever;
- prompt template;
- chat model;
- output parser;
- tracing or logging.

Conceptually:

```text
loader -> splitter -> embeddings -> vector store -> retriever -> prompt -> model -> parser
```

### 15.1 Why LangChain helps here

LangChain gives standard interfaces for these pieces. This means you can often swap one component for another:

- use one vector database locally, another in production;
- use one model provider now, another later;
- change the text splitter;
- add a reranker;
- add tracing;
- add tools.

The benefit is not that LangChain makes the concepts disappear. The benefit is that it gives you reusable building blocks once you understand the concepts.

---

## 16. RAG with agents

Basic RAG always retrieves before generation.

Agentic RAG allows the model to decide whether it needs retrieval, which query to use, and sometimes whether to retrieve again.

Basic RAG:

```text
Always retrieve -> answer
```

Agentic RAG:

```text
Question -> model decides search query -> retrieve -> inspect -> maybe retrieve again -> answer
```

Agentic RAG is more flexible, but also harder to control. It can be useful when:

- questions are complex;
- the user may need multiple sources;
- the first retrieval may not be enough;
- the system has multiple tools;
- the answer requires step-by-step investigation.

It can be risky when:

- tool calls are expensive;
- latency matters;
- the model may search badly;
- compliance requires predictable behavior.

Start with simple RAG. Move to agentic RAG only when simple RAG is not enough.

---

## 17. Evaluating RAG

You cannot judge a RAG system only by reading one nice answer. You need evaluation.

### 17.1 Retrieval evaluation

Ask: did the system retrieve the right chunks?

Metrics and checks:

- top-k accuracy;
- recall at k;
- manual relevance score;
- whether the gold source appears in retrieved results;
- whether irrelevant chunks appear too often.

Example test case:

```json
{
  "question": "What documents are needed for a student visa?",
  "expected_source": "student_visa_checklist.pdf",
  "expected_section": "Required documents"
}
```

If retrieval does not find the expected source, the generator will probably fail.

### 17.2 Answer evaluation

Ask: did the final answer correctly use the retrieved chunks?

Score:

- factual correctness;
- groundedness;
- completeness;
- citation quality;
- clarity;
- refusal when context is missing.

### 17.3 End-to-end evaluation

Ask: would this answer actually help the user?

This includes:

- retrieval;
- reasoning;
- formatting;
- source citation;
- user experience.

---

## 18. Common RAG failure modes

### Failure 1: The right chunk was never indexed

Cause: document missing, extraction failed, or chunking removed the section.

Fix: inspect ingestion pipeline and source coverage.

### Failure 2: The right chunk exists but retrieval misses it

Cause: poor embeddings, bad query, weak chunking, or missing keyword search.

Fix: try query rewriting, hybrid search, metadata filters, or reranking.

### Failure 3: Retrieval finds the right chunk, but the answer is wrong

Cause: weak prompt, too much irrelevant context, model ignores evidence, or conflicting chunks.

Fix: improve prompt, reduce noise, cite sources, add validation.

### Failure 4: The answer is correct but has no source

Cause: metadata missing or citation prompt missing.

Fix: store metadata and force source-aware output.

### Failure 5: User sees information they should not access

Cause: missing permission filtering.

Fix: apply access control before retrieval or during retrieval filtering.

---

## 19. Production design checklist

Before shipping RAG, check:

- Are all documents valid and current?
- Is text extraction reliable?
- Are chunks meaningful?
- Is metadata complete?
- Is access control enforced?
- Is retrieval tested separately?
- Are answers tested end-to-end?
- Does the system say when it does not know?
- Are sources shown to the user?
- Are logs stored safely?
- Is cost monitored?
- Is latency acceptable?
- Is there a plan for updating documents?

---

## 20. Mini project: build a study-book RAG assistant

### Goal

Build a chatbot that answers questions using this study book as the knowledge base.

### Data

Use the Markdown files in the `book/` folder.

### Indexing plan

1. Load all Markdown files.
2. Split by headings.
3. Store chapter title and section heading as metadata.
4. Embed each chunk.
5. Store chunks in a vector database.

### Query plan

1. User asks a question.
2. Retrieve top 5 chunks.
3. Build a grounded prompt.
4. Generate an answer.
5. Show chapter and section references.

### Example questions

- What is the difference between RAG and fine-tuning?
- Why does chunking matter?
- When should I use LangChain?
- What is reranking?
- How do I evaluate retrieval quality?

### Success criteria

The assistant should:

- answer from the study book;
- cite the chapter or section;
- refuse when the answer is not in the book;
- avoid making unsupported claims;
- be fast enough for interactive use.

---

## 21. RAG vs fine-tuning

RAG and fine-tuning solve different problems.

### Use RAG when:

- knowledge changes often;
- you need citations;
- you need private documents;
- you want to update knowledge without retraining;
- answers should be grounded in sources.

### Use fine-tuning when:

- you need a consistent style;
- you need a repeated classification behavior;
- you have many high-quality examples;
- the task is stable;
- prompting is not enough.

### Use both when:

- you need a model with specific behavior and access to external knowledge.

Example: a legal assistant may use fine-tuning for output style and RAG for retrieving current legal documents.

---

## 22. LangChain mental model

LangChain applications can be understood through five major concepts.

### 22.1 Models

The language model or chat model that generates outputs.

### 22.2 Prompts

Instructions and templates used to shape model behavior.

### 22.3 Retrievers

Components that fetch relevant information.

### 22.4 Tools

Functions the model or agent can call.

### 22.5 Chains or graphs

The control flow connecting steps together.

If you understand these five concepts, most LangChain examples become easier to read.

---

## 23. Study summary

RAG is not “put documents into ChatGPT.” It is a system design pattern.

A good RAG system needs:

- clean documents;
- thoughtful chunking;
- strong embeddings;
- vector or hybrid search;
- metadata;
- clear prompts;
- source citations;
- access control;
- evaluation;
- monitoring.

LangChain can help organize the system, but it does not remove the need to understand the system.

The most important idea in this chapter is:

```text
RAG quality = document quality + chunk quality + retrieval quality + prompt quality + evaluation quality
```

---

## 24. Exercises

### Exercise 1 — Explain RAG simply

Explain RAG to a non-technical friend using the open-book exam analogy.

### Exercise 2 — Design chunks

Take a one-page document and split it into chunks manually. Explain why you chose those boundaries.

### Exercise 3 — Metadata design

For a university visa PDF, define metadata fields that would help retrieval and citations.

### Exercise 4 — Failure analysis

A RAG system gives a wrong answer. The correct document exists in the database. List five possible causes.

### Exercise 5 — RAG vs fine-tuning

For each case, choose RAG, fine-tuning, direct prompting, or traditional code:

1. Answer questions from company policy PDFs.
2. Rewrite marketing copy in a fixed brand voice.
3. Calculate VAT from a known formula.
4. Classify support tickets into five categories.
5. Answer questions about recent internal announcements.

---

## 25. Exercise solutions

### Solution 1

RAG is like giving the AI an open book before asking it a question. Instead of guessing from memory, it searches the book, reads the relevant pages, and answers from those pages.

### Solution 2

Good chunks should preserve complete meaning. Split at headings, paragraphs, or complete rules. Avoid cutting a rule in half.

### Solution 3

Useful metadata fields include source file, page number, section heading, document date, language, visa type, country, and access level.

### Solution 4

Possible causes:

1. retrieval did not find the correct chunk;
2. chunking separated important context;
3. prompt did not force grounded answers;
4. model ignored the context;
5. conflicting outdated chunks were retrieved.

### Solution 5

1. Company policy PDFs: RAG.
2. Brand voice rewriting: fine-tuning or strong prompting.
3. VAT calculation: traditional code.
4. Ticket classification: traditional ML, fine-tuning, or structured prompting depending on scale.
5. Recent internal announcements: RAG.

---

## 26. Interview questions

1. What problem does RAG solve?
2. What is the difference between indexing time and query time?
3. Why is chunking important?
4. What is an embedding?
5. What does a vector database store?
6. Why is metadata important?
7. What is hybrid search?
8. What is reranking?
9. How do you evaluate retrieval quality?
10. How do you evaluate answer quality?
11. When would you use RAG instead of fine-tuning?
12. When would you use fine-tuning instead of RAG?
13. What can go wrong in a RAG system?
14. Why might LangChain be useful?
15. When should you avoid LangChain?

---

## 27. Glossary

**Agentic RAG**: A RAG system where an agent can decide when and how to retrieve information.

**Chunk**: A piece of a larger document used for retrieval.

**Chunk overlap**: Repeated text between neighboring chunks to preserve context.

**Embedding**: A numeric vector representing semantic meaning.

**Grounded answer**: An answer based on provided evidence rather than unsupported model memory.

**Hybrid search**: Search that combines keyword matching and semantic similarity.

**Indexing**: Preparing documents for retrieval by extracting, chunking, embedding, and storing them.

**LangChain**: A framework for building applications around language models, tools, retrieval, and agents.

**Metadata**: Extra information stored with chunks, such as source, page, date, and permissions.

**RAG**: Retrieval-Augmented Generation, a pattern where relevant information is retrieved and passed to a model before generation.

**Reranking**: Reordering retrieved results using a more precise relevance model.

**Retriever**: The component that finds relevant chunks for a query.

**Vector database**: A database optimized for storing and searching embeddings.

---

## 28. What to build next

To master this chapter, build a small RAG project:

1. Put three Markdown or PDF documents in a folder.
2. Extract and split the text.
3. Store chunks with metadata.
4. Implement retrieval.
5. Build a prompt that uses retrieved context.
6. Return answers with sources.
7. Create ten test questions.
8. Record which questions fail and why.

Do not aim for perfection first. Aim for observability: you should be able to see what was retrieved, what prompt was built, what answer was generated, and why the answer passed or failed.
