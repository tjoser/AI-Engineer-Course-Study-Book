# 12 — Agents, Evaluations, and Production AI

## What is an AI agent?

An AI agent is a system where a model can decide steps, use tools, inspect results, and continue toward a goal.

A simple chatbot only replies. An agent may:

- Search documents.
- Call APIs.
- Write files.
- Query databases.
- Use calculators.
- Ask for clarification.
- Plan multi-step tasks.
- Verify intermediate results.

## Agent loop

A typical agent loop:

1. Receive goal.
2. Decide next step.
3. Use a tool or produce output.
4. Observe result.
5. Decide whether more work is needed.
6. Finish with final answer.

## Tools

A tool is a function the model can call. Examples:

- Weather lookup.
- Calendar search.
- Database query.
- Email search.
- Calculator.
- Web search.
- File retrieval.

Tools make models more useful because they connect language reasoning to real actions and fresh data.

## Guardrails

Guardrails are rules and checks that keep the system safe and reliable.

Examples:

- Restrict what tools can be called.
- Validate tool arguments.
- Confirm before important actions.
- Block unsupported requests.
- Limit access by user permission.
- Log actions for review.

## Evaluation

Evaluation means measuring whether the AI system works well.

For LLM apps, evaluation can include:

- Correctness.
- Groundedness.
- Relevance.
- Completeness.
- Safety.
- Format validity.
- Latency.
- Cost.
- User satisfaction.

## Types of evaluation

### Manual review

Humans inspect outputs. Best for early development and nuanced quality.

### Golden dataset

A fixed set of test inputs with expected outputs or scoring rules.

### Automated checks

Code checks formatting, required fields, citations, or business rules.

### Model-based grading

Another model scores outputs using a rubric. Useful but should be calibrated and monitored.

## Production monitoring

Monitor:

- Request count.
- Error rate.
- Latency.
- Token usage.
- Cost.
- Retrieval hit quality.
- User feedback.
- Safety events.
- Model version.

## Versioning

Version everything:

- Prompts.
- Models.
- Retrieval settings.
- Chunking logic.
- Evaluation datasets.
- Tool definitions.
- Output schemas.

Without versioning, you cannot explain why behavior changed.

## Human-in-the-loop

Use human approval when the system takes important actions, handles sensitive data, or produces high-impact recommendations.

## Practice task

Design an agent that helps you apply for jobs.

Define:

- Goal.
- Tools.
- Data sources.
- Actions that require confirmation.
- Evaluation criteria.
- Logs to store.

## Interview questions

1. What is an AI agent?
2. What is a tool call?
3. Why do agents need guardrails?
4. How do you evaluate an LLM application?
5. What should be monitored in production?
