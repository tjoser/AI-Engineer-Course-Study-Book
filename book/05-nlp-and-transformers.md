# 05 — NLP and Transformers

## What is NLP?

Natural Language Processing is the area of AI focused on language: text, speech transcripts, documents, messages, search queries, summaries, translations, and conversations.

Before modern LLMs, many NLP systems were built from separate steps: cleaning text, extracting features, training a classifier, then returning a prediction. Modern LLMs combine many capabilities into one flexible model, but the basic ideas still matter.

## Common NLP tasks

- Text classification.
- Sentiment analysis.
- Named entity recognition.
- Translation.
- Summarization.
- Question answering.
- Semantic search.
- Text generation.
- Information extraction.

## Text preprocessing

Classic NLP often includes:

- Lowercasing.
- Removing noise.
- Splitting text into tokens.
- Removing stop words.
- Stemming or lemmatization.
- Turning words into numeric features.

Modern LLM apps usually do less manual preprocessing, but you still need careful cleaning when building search, retrieval, and document pipelines.

## Tokens

Models do not read text exactly like humans. They process tokens. A token may be a word, part of a word, punctuation, or whitespace-like unit depending on the tokenizer.

Tokenization matters because:

- Context windows are measured in tokens.
- Cost is often related to token usage.
- Long documents must be split into chunks.
- Different languages tokenize differently.

## Embeddings

An embedding is a numeric vector that represents meaning. Texts with similar meanings should have vectors that are close together.

Embeddings are useful for:

- Semantic search.
- Recommendations.
- Duplicate detection.
- Clustering.
- Retrieval-augmented generation.

## Transformers

Transformers are neural network architectures designed for sequence data. Their key idea is attention: the model learns which tokens are relevant to each other.

This is powerful because language meaning depends on relationships. The same word can mean different things depending on context.

## Attention intuition

In the sentence “The bank approved the loan because it had enough information,” the word “it” refers to the bank. Attention helps the model connect related tokens instead of reading each word independently.

## Encoder, decoder, and encoder-decoder models

### Encoder models

Good for understanding text. Example use cases: classification, embeddings, search.

### Decoder models

Good for generating text. Most chat-style LLMs are decoder-style models.

### Encoder-decoder models

Good for sequence-to-sequence tasks like translation and summarization.

## Practical AI engineering view

You do not need to implement a Transformer from scratch to build AI apps, but you should understand:

- Why token limits exist.
- Why embeddings support semantic search.
- Why context affects output.
- Why long documents need chunking.
- Why model outputs are probabilistic.

## Practice task

Take five job descriptions and five CV summaries. Create a manual similarity ranking. Then explain how embeddings could automate the matching.

## Interview questions

1. What is NLP?
2. What is tokenization?
3. What are embeddings used for?
4. Why are Transformers important?
5. What is the difference between semantic search and keyword search?
