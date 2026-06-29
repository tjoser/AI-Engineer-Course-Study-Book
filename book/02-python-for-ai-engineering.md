# 02 — Python for AI Engineering

## Why Python matters

Python is the default language for much AI engineering because the ecosystem is strong: NumPy, pandas, scikit-learn, PyTorch, Hugging Face, LangChain, FastAPI, notebooks, and many data tools.

You do not need to become a Python language expert before building AI apps, but you must be comfortable reading code, writing functions, handling files, calling services, and debugging errors.

## Core Python you need

### Variables and types

Important types:

- `str` for text.
- `int` and `float` for numbers.
- `bool` for true or false logic.
- `list` for ordered collections.
- `dict` for key-value data.
- `tuple` for fixed grouped values.
- `set` for unique values.

AI apps often pass data as dictionaries because JSON uses the same basic structure.

### Functions

Functions make logic reusable.

```python
def clean_text(text: str) -> str:
    return text.strip().lower()
```

A good AI engineer writes small functions for input validation, text cleaning, retrieval, model calls, and response formatting.

### Files

AI apps often read documents, prompts, datasets, or configuration files.

```python
from pathlib import Path

text = Path("notes.txt").read_text(encoding="utf-8")
```

### Exceptions

External services can fail. Files may be missing. Models may return unexpected output.

```python
try:
    result = run_model(prompt)
except Exception as error:
    result = {"error": str(error)}
```

In production, use structured logging and clear error responses.

## Python libraries for AI work

### NumPy

Used for arrays, vectors, matrices, and numerical operations. Embeddings are usually arrays of floating-point numbers.

### pandas

Used for tabular data: CSV files, spreadsheets, cleaning columns, filtering rows, and exploratory analysis.

### scikit-learn

Used for traditional machine learning: classification, regression, clustering, preprocessing, splitting data, pipelines, and metrics.

### PyTorch

Used for deep learning and model training. Many open-source models can run through PyTorch.

### FastAPI

Used to turn AI logic into a backend service.

### Pydantic

Used for validating inputs and outputs, especially useful when building structured services around LLMs.

## AI backend structure

A clean AI backend usually has:

```text
app/
  main.py
  config.py
  schemas.py
  services/
    llm.py
    retrieval.py
    prompts.py
  tests/
```

## Practice task

Create a Python script that:

1. Reads a text file.
2. Splits it into paragraphs.
3. Counts words per paragraph.
4. Returns the longest paragraph.
5. Saves the result as JSON.

## Beginner mistakes

- Writing one giant script instead of small functions.
- Ignoring exceptions.
- Not using virtual environments.
- Not pinning package versions.
- Mixing business logic, prompts, and HTTP routes in one place.

## Interview questions

1. Why is Python popular for AI engineering?
2. What is the difference between a list and a dictionary?
3. Why are virtual environments important?
4. How would you structure a Python AI backend?
5. How do you handle service failures safely?
