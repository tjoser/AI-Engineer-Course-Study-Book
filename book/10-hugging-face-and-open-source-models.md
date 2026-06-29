# 10 — Hugging Face and Open-Source Models

## Why Hugging Face matters

Hugging Face is one of the most important ecosystems for open-source AI. It provides model hosting, datasets, tokenizers, demos, and libraries such as Transformers.

For AI engineers, Hugging Face is useful because you can quickly find and test pretrained models for text, vision, audio, and multimodal tasks.

## Transformers library

The Transformers library gives developers tools for using pretrained models for inference and training.

Common tasks:

- Text generation.
- Classification.
- Summarization.
- Translation.
- Question answering.
- Automatic speech recognition.
- Image classification.
- Multimodal generation.

## Pipelines

A pipeline is a simple interface for common tasks.

Example concept:

```python
from transformers import pipeline

classifier = pipeline("sentiment-analysis")
result = classifier("This course is useful.")
```

Pipelines are great for learning and prototypes. For production, you may need more control over batching, latency, hardware, and model configuration.

## Model cards

A model card explains important details about a model:

- Intended use.
- Training data notes.
- License.
- Limitations.
- Evaluation results.
- Bias and risk notes.
- How to run it.

Always read the model card before using an open-source model.

## Datasets

Datasets are used for training, fine-tuning, and evaluation. Good datasets must match the problem you actually care about.

Check:

- Size.
- Format.
- License.
- Language.
- Quality.
- Label definitions.
- Collection method.
- Bias risks.

## Open-source vs hosted models

### Open-source models

Pros:

- More control.
- Can run locally or on your own servers.
- Potential privacy benefits.
- Customization options.

Cons:

- Infrastructure responsibility.
- Hardware cost.
- Deployment complexity.
- Monitoring and updates are your job.

### Hosted models

Pros:

- Easy to start.
- Managed infrastructure.
- Strong models available quickly.
- Less operational burden.

Cons:

- Usage cost.
- Rate limits.
- Vendor dependency.
- Data governance questions.

## Fine-tuning

Fine-tuning means training a pretrained model further on task-specific examples.

Use fine-tuning when:

- You have high-quality examples.
- Prompting is not enough.
- You need consistent style or classification.
- The task repeats at scale.

Do not fine-tune before trying strong prompting, retrieval, better context, or simpler deterministic logic.

## Practice task

Pick three models from Hugging Face and compare:

- Task.
- License.
- Input/output format.
- Model size.
- Limitations.
- Whether you would use it in production.

## Interview questions

1. What is Hugging Face used for?
2. What is a model card?
3. What is the difference between a hosted and self-hosted model?
4. When should you fine-tune?
5. Why is licensing important for open-source AI models?
