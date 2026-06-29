# 04 — Neural Networks and Deep Learning

## What is a neural network?

A neural network is a model made of layers of mathematical units. Each unit transforms input values into output values. During training, the network updates its parameters so its predictions become closer to the target outputs.

The basic idea is simple:

1. Input data goes into the network.
2. Layers transform the data.
3. The network makes a prediction.
4. A loss function measures the error.
5. Backpropagation updates the weights.
6. The process repeats many times.

## Key terms

### Weight

A learnable number that controls how strongly one signal affects another.

### Bias

A learnable offset added to a layer output.

### Activation function

A function that adds non-linearity. Without non-linearity, deep networks would behave like simpler linear models.

Common activations include ReLU, sigmoid, tanh, and softmax.

### Loss function

A function that measures how wrong the prediction is.

Examples:

- Cross-entropy for classification.
- Mean squared error for regression.

### Optimizer

An algorithm that updates model weights to reduce loss. Adam and SGD are common examples.

## Why deep learning became powerful

Deep learning became practical because of:

- More data.
- Better GPUs.
- Better architectures.
- Better training techniques.
- Open-source frameworks.
- Large pretrained models.

## Common architecture types

### Feedforward networks

Basic networks where data flows from input to output.

### Convolutional neural networks

Historically important for images and visual pattern recognition.

### Recurrent neural networks

Older sequence models used for text and time series. They were largely replaced in NLP by Transformers.

### Transformers

The architecture behind modern LLMs. Transformers use attention to model relationships between tokens efficiently.

## Training vs inference

### Training

Training means updating model parameters using data. This can be expensive.

### Inference

Inference means using a trained model to make predictions or generate outputs. Most AI engineers spend more time building inference applications than training foundation models from scratch.

## Pretraining, fine-tuning, and prompting

### Pretraining

Large models learn general patterns from huge datasets.

### Fine-tuning

A pretrained model is further trained on a smaller, more specific dataset.

### Prompting

The model weights stay the same, but you guide behavior using instructions and context.

## Practical rule

Do not train a model from scratch unless you have a strong reason, enough data, enough budget, and a clear evaluation method.

Most AI products are built by combining pretrained models, prompts, retrieval, tools, and backend systems.

## Practice task

Explain the lifecycle of an LLM-powered feature using these words:

- Input
- Tokens
- Model
- Inference
- Output
- Evaluation

## Interview questions

1. What is a neural network?
2. What is the difference between training and inference?
3. Why are Transformers important?
4. What is fine-tuning?
5. Why do most AI engineers use pretrained models?
