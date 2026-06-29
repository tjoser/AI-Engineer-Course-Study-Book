# 07 — Prompt Engineering

## What is prompt engineering?

Prompt engineering is writing effective instructions and context so a model produces useful, consistent output.

A prompt is not only the final user message. In real applications, the prompt may include:

- System or developer instructions.
- User request.
- Retrieved context.
- Examples.
- Output schema.
- Tool descriptions.
- Conversation history.

## Basic prompt structure

A strong prompt often includes:

1. Role: what the model should act as.
2. Task: what it must do.
3. Context: what information it should use.
4. Constraints: what it must avoid.
5. Format: how the answer should be returned.
6. Examples: optional demonstrations of correct behavior.

## Bad prompt

```text
Summarize this.
```

## Better prompt

```text
You are helping a software engineer study AI engineering.
Summarize the text into:
1. Main idea
2. Key terms
3. Practical example
4. Three review questions
Use simple language and do not invent facts.
```

## Zero-shot prompting

The model gets only the instruction, no examples.

Use it when the task is simple or the model already understands the pattern.

## Few-shot prompting

The prompt includes examples of inputs and ideal outputs.

Use it when you need a specific style, classification rule, or output pattern.

## Asking for explanations

You can ask the model to explain its answer, but keep the explanation short and focused. In production, prefer outputs that can be validated by code, such as JSON fields, confidence labels, or citations to provided context.

## Prompting for structured output

When connecting AI to software, prefer structured output.

```json
{
  "answer": "...",
  "confidence": "low | medium | high",
  "missing_information": ["..."]
}
```

Structured output helps with testing, storage, UI rendering, and downstream logic.

## Prompting with context

When giving the model documents or retrieved chunks, clearly separate instructions from context.

```text
Task: Answer the user using only the context below.

Context:
---
...
---

User question:
...
```

## Common mistakes

- Vague instructions.
- Too much irrelevant context.
- No output format.
- No examples for complex classification.
- Asking for facts without sources.
- Forgetting edge cases.
- Not testing prompts after model upgrades.

## Prompt testing

Create a small test set of inputs and expected behavior.

For each prompt change, test:

- Normal case.
- Ambiguous case.
- Long input.
- Missing information.
- User asks something outside scope.
- Conflicting context.

## Practice task

Write a prompt that extracts job requirements from a job post into JSON:

- title
- company
- location
- required skills
- preferred skills
- seniority
- summary

## Interview questions

1. What makes a prompt reliable?
2. What is few-shot prompting?
3. Why is structured output useful?
4. How do you test prompts?
5. Why should prompts be versioned in production?
