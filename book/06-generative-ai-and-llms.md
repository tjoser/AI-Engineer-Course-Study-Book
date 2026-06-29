# 06 — Generative AI and Large Language Models

## What is generative AI?

Generative AI creates new content from learned patterns. It can generate text, code, images, audio, video, summaries, plans, and structured data.

For software engineers, the most important category is the Large Language Model.

## What is an LLM?

A Large Language Model is a model trained on huge amounts of text and code to predict and generate sequences of tokens. Because language contains knowledge, reasoning patterns, instructions, examples, and code, LLMs can perform many tasks through natural-language interaction.

## What LLMs are good at

- Drafting and rewriting text.
- Summarizing documents.
- Explaining code.
- Generating code snippets.
- Classifying language inputs.
- Extracting structured data.
- Answering questions with provided context.
- Planning and tool usage when connected to tools.

## What LLMs are weak at

- Guaranteed factual accuracy without grounding.
- Exact arithmetic unless tools are used.
- Knowing private or recent data unless provided.
- Consistent output without clear instructions.
- Understanding your business rules unless you define them.
- Safe autonomous action without guardrails.

## Hallucination

Hallucination means the model produces an answer that sounds confident but is false or unsupported.

Ways to reduce hallucination:

- Provide relevant context.
- Use retrieval from trusted documents.
- Ask for citations to sources.
- Use structured outputs.
- Add validation logic.
- Use tools for calculations and database lookups.
- Evaluate outputs with test cases.

## Context window

The context window is the amount of information the model can consider in one request. It includes instructions, conversation history, retrieved documents, tool results, and the user message.

More context is not always better. Bad context can confuse the model. Good AI engineering means choosing the right context.

## Temperature

Temperature controls randomness. Lower temperature usually gives more consistent outputs. Higher temperature can produce more varied or creative outputs.

For production systems, start low unless creativity is a key requirement.

## Structured outputs

Many AI apps need JSON or predictable fields, not free-form prose.

Example output shape:

```json
{
  "category": "billing",
  "priority": "high",
  "summary": "Customer asks about an unexpected charge."
}
```

Structured outputs make the model easier to connect to backend logic.

## Model selection

Choose based on:

- Accuracy needs.
- Latency.
- Cost.
- Context length.
- Tool support.
- Privacy and compliance requirements.
- Multimodal needs.

Use smaller models for simple classification or formatting. Use stronger models for complex reasoning, ambiguous tasks, or high-value workflows.

## Practice task

Design a model call for a customer-support assistant. Define:

- System instruction.
- User input.
- Context data.
- Output format.
- Failure behavior.
- Evaluation metric.

## Interview questions

1. What is an LLM?
2. What is hallucination?
3. How does RAG reduce hallucination?
4. What is a context window?
5. How do you choose between a small and large model?
