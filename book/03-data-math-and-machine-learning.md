# 03 — Data, Math, and Machine Learning Basics

## Why data matters

Models learn from data. If the data is messy, biased, incomplete, outdated, or unrelated to the real problem, the model will produce weak results.

AI engineering starts with this question: what data does the system need to make a useful decision or generate a useful answer?

## Core vocabulary

### Dataset

A collection of examples used for analysis, training, validation, or testing.

### Feature

An input variable used by a model.

Example: for predicting house prices, features could be area, number of rooms, city, and building age.

### Label

The target output the model learns to predict.

Example: the actual house price.

### Training set

The data used to teach the model.

### Validation set

The data used during development to tune choices.

### Test set

The data reserved for final evaluation.

## Supervised learning

Supervised learning uses examples where both input and correct output are known.

Main task types:

- Classification: predict a category.
- Regression: predict a number.

Examples:

- Classify support tickets by department.
- Predict delivery time.
- Predict customer churn.

## Unsupervised learning

Unsupervised learning finds structure without explicit labels.

Main task types:

- Clustering: group similar items.
- Dimensionality reduction: compress data while preserving useful structure.
- Anomaly detection: find unusual examples.

## Reinforcement learning

Reinforcement learning trains an agent to take actions in an environment and receive rewards or penalties. It is important historically and in some advanced AI systems, but many business AI apps do not require you to train reinforcement learning models yourself.

## Overfitting and generalization

A model overfits when it memorizes training examples but performs poorly on new examples.

Good models generalize: they perform well on new data from the same real-world problem.

Ways to reduce overfitting:

- Use more representative data.
- Use simpler models when possible.
- Use validation and test sets.
- Regularize the model.
- Avoid leaking target information into features.

## Evaluation metrics

### Accuracy

Percentage of predictions that are correct. Useful when classes are balanced.

### Precision

Of all items predicted positive, how many were actually positive?

### Recall

Of all actual positive items, how many did the model find?

### F1 score

A balance between precision and recall.

### Mean Absolute Error

Average absolute difference between predicted number and true number. Useful for regression.

## Practical AI engineering view

Traditional ML is still useful. Not every problem needs an LLM. Use the simplest reliable solution:

- Rules when logic is clear.
- Search when exact retrieval is enough.
- Classical ML when structured prediction is enough.
- LLMs when language understanding, generation, reasoning, or flexible interaction is needed.

## Practice task

Take any CSV dataset and identify:

1. The target label.
2. Five possible features.
3. The task type.
4. The metric you would use.
5. What could make the data unreliable.

## Interview questions

1. What is the difference between a feature and a label?
2. Why do we split data into train, validation, and test sets?
3. What is overfitting?
4. When is accuracy a bad metric?
5. When would you choose traditional ML instead of an LLM?
