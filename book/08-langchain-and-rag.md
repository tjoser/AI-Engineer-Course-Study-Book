# 08 — LangChain and RAG Applications

## Why frameworks exist

LLM apps often repeat the same patterns:

- Receive a user message.
- Add instructions.
- Retrieve context.
- Call a model.
- Parse output.
- Call tools.
- Track history.
- Log traces.
- Evaluate results.

Frameworks help organize these patterns so you do not build everything from scratch each time.

## What LangChain is useful for

LangChain helps developers compose applications around language models. It provides common building blocks for models, messages, tools, retrieval, agents, middleware, tracing, and integration with other providers.

Use it when you want structure and reusable components. Avoid overcomplicating simple apps that only need one model call.

## RAG meaning

RAG means Retrieval-Augmented Generation.

Instead of asking the model to answer from memory, you retrieve relevant information from your own documents or database and include it in the prompt.

## Basic RAG pipeline

1. Collect documents.
2. Split documents into chunks.
3. Convert chunks into embeddings.
4. Store embeddings in a vector database.
5. User asks a question.
6. Convert the question into an embedding.
7. Retrieve similar chunks.
8. Send question plus chunks to the LLM.
9. Return an answer with sources.

## Why RAG is useful

RAG helps when:

- The model does not know your private data.
- The data changes often.
- You need answers grounded in documents.
- You want citations.
- You want to avoid retraining.

## Chunking

Chunking means splitting documents into smaller pieces. Good chunks preserve meaning.

Bad chunking can break important context. Very small chunks may lose meaning. Very large chunks may waste tokens and reduce retrieval quality.

Common chunking strategies:

- Fixed-size chunks.
- Paragraph-based chunks.
- Heading-based chunks.
- Semantic chunks.
- Overlapping chunks.

## Retrieval quality

The answer quality depends heavily on retrieval quality. If the retriever finds irrelevant context, the LLM may answer poorly.

Improve retrieval by:

- Cleaning documents.
- Adding metadata.
- Improving chunking.
- Using hybrid search.
- Reranking retrieved results.
- Evaluating with real user questions.

## RAG answer prompt

A good RAG prompt tells the model:

- Use only the provided context.
- Say when context is insufficient.
- Cite the sources or chunk identifiers.
- Keep the answer concise.
- Do not invent missing details.

## When RAG is not enough

RAG is not magic. It may fail when:

- Documents are outdated.
- The needed answer requires calculation.
- The answer requires multiple tool calls.
- The question requires access control.
- The retrieved chunks are incomplete.
- The user asks something outside the knowledge base.

## Practice task

Build a mini RAG plan for university visa documents:

1. Documents to ingest.
2. Chunking strategy.
3. Metadata fields.
4. Example questions.
5. Evaluation method.
6. Failure response.

## Interview questions

1. What is RAG?
2. Why use RAG instead of fine-tuning?
3. What makes chunking hard?
4. How do you evaluate a RAG system?
5. What is the difference between retrieval and generation?
