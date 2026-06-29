# 11 — APIs, Backends, and Deployment

## Why backend engineering matters

Most useful AI features live inside normal software systems. The model is only one part. A production AI app also needs authentication, databases, file storage, APIs, logging, monitoring, security, billing, and user experience.

## Typical AI backend flow

1. Receive request from UI or mobile app.
2. Validate input.
3. Load user/session data.
4. Retrieve relevant context if needed.
5. Build prompt or model input.
6. Call model.
7. Parse output.
8. Validate output.
9. Save logs and result.
10. Return response to the client.

## FastAPI-style service design

Good structure:

```text
app/
  main.py
  routes/
    chat.py
    documents.py
  services/
    model_service.py
    retrieval_service.py
    evaluation_service.py
  schemas/
    requests.py
    responses.py
  config.py
  tests/
```

## Environment configuration

Keep configuration separate from code:

- model name
- service keys
- database URL
- logging level
- allowed origins
- feature flags

Use environment variables and deployment secrets. Do not put private values directly in source code.

## Latency

Users care about speed. AI apps can be slow because of model calls, retrieval, reranking, long prompts, or tool calls.

Ways to improve latency:

- Use smaller models when possible.
- Stream responses.
- Cache repeated results.
- Retrieve fewer but better chunks.
- Avoid unnecessary context.
- Run independent operations in parallel.
- Use background processing for long jobs.

## Cost

AI cost often depends on model choice and token usage.

Control cost by:

- Tracking input and output tokens.
- Using smaller models for simple tasks.
- Summarizing long histories.
- Caching.
- Setting max output limits.
- Monitoring usage per user or feature.

## Reliability

AI services should handle:

- Timeouts.
- Empty outputs.
- Invalid JSON.
- Model refusals.
- Rate limits.
- Irrelevant retrieval results.
- User input outside scope.

## Security and privacy

Think carefully about:

- Private documents.
- Access control.
- Prompt injection.
- Tool permissions.
- Data retention.
- Logging sensitive text.
- User consent.

## Deployment options

Common options:

- Render, Railway, Fly.io, or Heroku-like platforms for small projects.
- AWS, Azure, or Google Cloud for production systems.
- Docker containers for portability.
- Serverless functions for lightweight tasks.
- Kubernetes for complex systems.

## Practice task

Design an API endpoint for a PDF Q&A system.

Include:

- Request body.
- Response body.
- Error cases.
- Logs to store.
- Metrics to monitor.
- Security checks.

## Interview questions

1. What belongs outside the model call in an AI backend?
2. How do you reduce AI API latency?
3. How do you control token cost?
4. What is prompt injection?
5. Why should AI outputs be validated?
