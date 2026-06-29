# Review Questions

Use these questions after finishing each chapter. Answer without looking first, then review the chapter.

## 01 — AI Engineering Roadmap

1. Define AI in one sentence.
2. Define machine learning in one sentence.
3. Define deep learning in one sentence.
4. Define generative AI in one sentence.
5. What does an AI engineer build?
6. Why is AI engineering not only model training?
7. What are the main skills of an AI engineer?
8. Give three examples of AI-powered products.
9. Why is evaluation important?
10. What is the difference between research and product engineering?

## 02 — Python for AI Engineering

1. Why is Python common in AI?
2. What Python data types appear often in AI APIs?
3. Why are functions important in AI code?
4. What is the purpose of exception handling?
5. What is NumPy used for?
6. What is pandas used for?
7. What is scikit-learn used for?
8. What is FastAPI used for?
9. Why should prompts and service logic be separated?
10. What makes a backend structure clean?

## 03 — Data, Math, and Machine Learning

1. What is a dataset?
2. What is a feature?
3. What is a label?
4. What is supervised learning?
5. What is unsupervised learning?
6. What is overfitting?
7. What is generalization?
8. When is accuracy misleading?
9. What is the difference between precision and recall?
10. When should you use traditional ML instead of an LLM?

## 04 — Neural Networks and Deep Learning

1. What is a neural network?
2. What are weights?
3. What is an activation function?
4. What is a loss function?
5. What is an optimizer?
6. Why did deep learning become practical?
7. What is the difference between training and inference?
8. What is pretraining?
9. What is fine-tuning?
10. Why are Transformers important?

## 05 — NLP and Transformers

1. What is NLP?
2. Name five NLP tasks.
3. What is tokenization?
4. Why do token limits matter?
5. What is an embedding?
6. What is semantic search?
7. What is attention?
8. What is an encoder model good for?
9. What is a decoder model good for?
10. Why do long documents need chunking?

## 06 — Generative AI and LLMs

1. What is generative AI?
2. What is an LLM?
3. What are LLMs good at?
4. What are LLMs weak at?
5. What is hallucination?
6. How can hallucination be reduced?
7. What is a context window?
8. What does temperature control?
9. Why are structured outputs useful?
10. How do you choose a model?

## 07 — Prompt Engineering

1. What is prompt engineering?
2. What are the parts of a strong prompt?
3. What is zero-shot prompting?
4. What is few-shot prompting?
5. Why should context be separated from instructions?
6. Why is JSON output useful?
7. What are common prompt mistakes?
8. How do you test a prompt?
9. Why should prompts be versioned?
10. What does it mean to avoid inventing facts?

## 08 — LangChain and RAG

1. Why do LLM frameworks exist?
2. What is LangChain used for?
3. What is RAG?
4. What are the steps of a RAG pipeline?
5. Why does chunking matter?
6. What is retrieval quality?
7. How can retrieval be improved?
8. When is RAG useful?
9. When is RAG not enough?
10. What should a RAG prompt include?

## 09 — Embeddings and Vector Databases

1. What is an embedding?
2. Why does semantic search need embeddings?
3. What is a vector database?
4. What metadata should be stored with chunks?
5. What is cosine similarity?
6. What is reranking?
7. Why combine keyword and semantic search?
8. What are common vector search mistakes?
9. What is pgvector?
10. How do you test retrieval quality?

## 10 — Hugging Face and Open-Source Models

1. What is Hugging Face?
2. What is the Transformers library?
3. What is a pipeline?
4. What is a model card?
5. Why does licensing matter?
6. What are the benefits of open-source models?
7. What are the drawbacks of self-hosting models?
8. When is fine-tuning useful?
9. What should you check before using a dataset?
10. What is the difference between prototype and production model usage?

## 11 — APIs, Backends, and Deployment

1. What happens before and after the model call in an AI backend?
2. Why validate input?
3. Why validate output?
4. How can latency be reduced?
5. How can cost be controlled?
6. What should be logged?
7. What are common AI service failure cases?
8. What is prompt injection?
9. Why is access control important?
10. What deployment options can be used for AI APIs?

## 12 — Agents, Evaluations, and Production AI

1. What is an AI agent?
2. What is a tool?
3. What is an agent loop?
4. What are guardrails?
5. What is a golden dataset?
6. What can automated checks validate?
7. What is model-based grading?
8. What should be monitored in production?
9. Why version prompts and retrieval settings?
10. When should a human stay in the loop?

## Final self-test

Explain this full system in your own words:

A user uploads PDF documents. The backend extracts text, chunks it, embeds chunks, stores them in a vector database, retrieves relevant chunks for each question, sends the chunks and question to an LLM, validates the output, returns an answer with sources, logs the request, and monitors cost and quality.

Your explanation should mention:

- chunking
- embeddings
- vector database
- retrieval
- prompt
- context window
- hallucination
- structured output
- evaluation
- monitoring
