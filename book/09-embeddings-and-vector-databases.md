# 09 — Embeddings and Vector Databases

## What is an embedding?

An embedding is a list of numbers that represents the meaning of text, images, audio, or other data. For text, the goal is that similar meanings produce nearby vectors.

Example:

- “How do I apply for a student visa?”
- “What are the student visa requirements?”

These two sentences use different words but have similar meaning, so their embeddings should be close.

## Why embeddings matter

Embeddings allow software to search by meaning instead of only exact keywords.

Use cases:

- Semantic search.
- Document Q&A.
- Recommendation systems.
- Similarity matching.
- Clustering.
- Duplicate detection.
- RAG.

## Keyword search vs semantic search

### Keyword search

Finds exact or close word matches.

Good for names, IDs, exact phrases, and filters.

### Semantic search

Finds meaning similarity.

Good for natural-language questions and documents with different wording.

Best production systems often combine both.

## Vector database

A vector database stores embeddings and makes similarity search fast.

Common options include:

- FAISS for local experiments.
- Chroma for simple local RAG projects.
- Pinecone for managed vector search.
- Weaviate for vector and hybrid search.
- Milvus for scalable open-source vector search.
- pgvector when you want vectors inside PostgreSQL.

## Metadata

Store metadata with each chunk:

- source file
- page number
- section title
- created date
- access level
- document type
- language

Metadata helps filtering and citation.

## Similarity search

Common similarity measures:

- Cosine similarity.
- Dot product.
- Euclidean distance.

For most app builders, the key point is simple: the search returns chunks with vectors closest to the query vector.

## Reranking

Initial vector search may return approximate matches. A reranker can reorder results by deeper relevance.

Reranking is useful when:

- Many chunks are similar.
- The domain is technical.
- The first retrieval step is noisy.
- Answer accuracy matters.

## Practical design choices

When building a vector search system, decide:

1. Embedding model.
2. Chunk size.
3. Chunk overlap.
4. Metadata fields.
5. Vector database.
6. Number of retrieved chunks.
7. Reranking strategy.
8. Citation format.
9. Refresh schedule.

## Common mistakes

- Storing chunks without source metadata.
- Using huge chunks.
- Not cleaning documents.
- Not testing retrieval separately from generation.
- Assuming the vector database alone solves answer quality.
- Forgetting access control.

## Practice task

Create a small document search design for your CV and job descriptions:

- What will each chunk represent?
- What metadata will you store?
- What question examples will you test?
- How will you know retrieval is good?

## Interview questions

1. What is an embedding?
2. Why do vector databases help RAG?
3. What metadata should you store with chunks?
4. What is reranking?
5. Why combine keyword and semantic search?
