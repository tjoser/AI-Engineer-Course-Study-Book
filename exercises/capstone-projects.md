# Capstone Projects

Use these projects to turn the book into portfolio evidence.

## Project 1 — CV and Job Match Assistant

### Goal

Build an AI tool that compares your CV with job descriptions and gives a useful match report.

### Features

- Upload or paste CV text.
- Paste job description.
- Extract required skills.
- Extract your matching skills.
- Identify gaps.
- Suggest a short LinkedIn message.
- Return structured JSON and a human-readable report.

### Technical requirements

- Python backend.
- Structured output.
- Prompt tests.
- Error handling.
- Optional: Flutter or web UI.

### Evaluation

Test on at least 10 job posts and manually score:

- Did it extract skills correctly?
- Did it avoid inventing experience?
- Were gap suggestions useful?

## Project 2 — PDF RAG Chatbot

### Goal

Build a chatbot that answers questions from uploaded PDFs.

### Features

- Upload documents.
- Split text into chunks.
- Store embeddings.
- Ask questions.
- Retrieve relevant chunks.
- Generate grounded answers.
- Show source references.

### Technical requirements

- PDF parser.
- Embedding model.
- Vector database.
- RAG prompt.
- API endpoint.
- Basic UI.

### Evaluation

Create 20 questions:

- 10 easy questions with direct answers.
- 5 questions requiring multiple sections.
- 5 questions where the answer is not in the documents.

The system should say when it does not have enough context.

## Project 3 — AI Backend Support Classifier

### Goal

Classify incoming support messages and route them.

### Features

- Classify category.
- Estimate priority.
- Summarize the issue.
- Extract required follow-up.
- Return JSON.

### Technical requirements

- FastAPI endpoint.
- Pydantic schema.
- Test cases.
- Logging.
- Prompt versioning.

### Evaluation

Use a small test set and measure:

- Category accuracy.
- JSON validity.
- Priority consistency.
- Failure handling.

## Project 4 — Tool-Using Study Agent

### Goal

Build an agent that helps you study AI engineering.

### Features

- Reads chapter notes.
- Generates quizzes.
- Tracks weak topics.
- Suggests next study task.
- Uses a calculator or search tool when needed.

### Guardrails

- Do not claim mastery without quiz evidence.
- Do not answer from outside sources unless allowed.
- Ask for confirmation before deleting notes or changing progress.

## Project 5 — AI App Production Checklist

### Goal

Create a checklist app for reviewing AI features before launch.

### Sections

- Prompt versioning.
- Model choice.
- Retrieval quality.
- Evaluation dataset.
- Safety checks.
- Monitoring.
- Cost controls.
- Privacy review.
- Human escalation.

## Suggested GitHub README for each project

Each project should include:

- Problem statement.
- Architecture diagram or text architecture.
- Setup instructions.
- Environment variables needed.
- Example requests and responses.
- Evaluation method.
- Known limitations.
- Future improvements.
