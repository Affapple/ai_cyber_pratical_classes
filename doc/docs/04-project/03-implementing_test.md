# Adding AI Tests

This document provides guidelines for adding AI tests to the evaluation module of the A4S project.
It covers the structure of tests, how to implement them, and how to run them.

## Test categories

Tests are categorized based on the type of inputs they receive and the specific aspects of the AI model they evaluate.

For tabular data, tests are organized into the following categories:

- **Data tests**: These tests focus on the integrity and quality of the input data.
- **Model tests**: These tests evaluate the performance and behavior of the AI model itself.
- **Prediction tests**: These tests assess the accuracy and reliability of the model's predictions.

Each category is represented by a module named `[category]_metric_registry.py` within the `a4s-eval/a4s_eval/metric_registries` modules.

## Test structure

Tests are implemented as functions that adhere to a specific protocol defined for each category.
At execution, the evaluation module dynamically discovers and runs these test functions based on the category of the evaluation being performed.
This follows the inversion of control principle, where the framework calls the test functions rather than the other way around.

Each test is defined as an annotated function within the `a4s-eval/a4s_eval/metrics/[category]_metrics/<metric_name>_metric.py` file corresponding to its category.

The test function signatures correspond to the protocol defined in the respective evaluator module `a4s_eval.metric_registries.[category]_metric_registry.py`.

Here is an example of a test function signature for a data test:

```python
class DataMetric(Protocol):
    def __call__(
        self, datashape: DataShape, reference: Dataset, evaluated: Dataset
    ) -> list[Metric]:
        """Run a specific data evaluation.

        Args:
            datashape: The datashape of the project
            reference: The reference dataset to run the evaluation.
            evaluated: The evaluated dataset.

        """
        raise NotImplementedError
```

Here is an example of a test function:

```python
from a4s_eval.metric_registries.data_metric_registry import data_metric

@data_metric(name="No Missing Values")
def test_no_missing_values(
    datashape: DataShape, reference: Dataset, evaluated: Dataset
) -> list[Measure]:
    """Test that there are no missing values in the evaluated dataset.
    # Implementation of the test
```

Each test function must return a list of `a4s_eval.data_model.measure.Measure` objects, which encapsulate the results of the test.

If a test encounters an error during execution, it should raise an exception.

## Running tests

Tests are meant to be run as part of the evaluation process within the A4S project.

However, during development, you might want to run them in isolation, locally or within a CI pipeline.

We provide semi-realistic datasets and models  that can be used to test your evaluation.

We also provide two basic smoke test for your evaluation, where we simply run all autodiscovered evaluation on the semi-realistic datasets and models (see `a4s-eval/tests/data`): 

- the evaluation runs without errors
- the evaluation returns some metrics.

You can run these tests using `pytest`:

```bash
uv run pytest tests/metrics/[category]_metrics/test_execute.py
```

## Adding your own tests

Feel free to add more specific tests for your evaluation in the `tests/metrics/[category]_metrics/test_<metric_name>.py` file.
