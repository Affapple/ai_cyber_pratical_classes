# Implementing Accuracy Metric in A4S

This document provides guidelines on how to implement accuracy tests within the A4S evaluation framework as a simple example of adding AI tests.

## Overview

Accuracy tests are designed to evaluate the performance of AI models by comparing their predictions against reference data.
Accuracy is defined as the ratio of correct predictions to the total number of predictions.

Altough this test could fall under the prediction metric category, we will use the Model Metric category to illustrate how to add a new metric that has access to the model object.
This will be useful for more complex metric implementations that require access to the model's internal state or parameters (and for your project).

## Metric structure

You must implement the accuracy metric as a function that adheres to the protocol defined in the `a4s_eval.metric_registries.model_metric_registry.ModelMetric` class.
This protocol defines the expected inputs and outputs for the metric function.

Using the annotation `@model_metric`, you can register your metric function within the A4S evaluation framework.
Here is an example of an accuracy metric function:

```python
@model_metric(name="accuracy")
def accuracy(
    datashape: DataShape,
    model: Model,
    dataset: Dataset,
    functional_model: FunctionalModel,
) -> list[Measure]:
```

Sklearn `accuracy_score` function is not part of the dependencies of A4S, so you need to implement it yourself.

## Test your metric

Once you have implemented the accuracy metric, you can test it by running A4S model metric test.

```bash
uv run pytest tests/metrics/model_metrics
```

This will execute the tests in the specified directory, including the accuracy metric test you have added.

It also calls the save measure function to save the results of the accuracy metric evaluation in `tests/data/measures/accuracy.csv`.

## Update the test suite

**Duplicate** the test function `tests.metrics.model_metrics.test_execute.test_data_metric_registry_contains_evaluator` and modify it to call the accuracy metric by batch of 10000 inputs.

To do so, you can override the `test_dataset.data: pd.DataFrame` object within the test function.

## Plot the accuracy results

You can visualize the results of the accuracy metric (in `tests/data/measures/accuracy.csv`) using matplotlib or any other plotting library of your choice.
After the batching, we expect multiple datapoint present in this file.
