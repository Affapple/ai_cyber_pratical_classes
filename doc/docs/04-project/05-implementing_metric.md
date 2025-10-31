# Implementing an arbitrary metric

This document provides guidelines on how to implement custom metrics within the A4S evaluation framework. Metrics are used to evaluate the performance of AI models based on specific criteria.

## Steps to implement a custom metric

1. **Define the requirements of your metric**: Determine what data and model information your metric will need to compute its results.\

For instance, data metrics may only require access to the dataset, while model metrics may need access to the model itself. It is also important to identify the type of models your metric will support (e.g., classification, regression, text generation, etc.).

2. **Identify the appropriate metric registry**: Based on the requirements defined in step 1, choose the appropriate metric registry to implement your metric. A4S provides different registries for various types of metrics, such as data metrics and model metrics.

The registry you choose will determine the inputs your metric function will receive.

You can find the available metric registries in the submodules of `a4s_eval.metric_registries` module, each designed for a specific type of metric.

The first `Protocol` class defined in each registry module outlines the expected inputs and outputs for metric functions registered in that registry.

For example, the `a4s_eval.metric_registries.model_metric_registry.ModelMetric` class defines the protocol for model metrics, the one you used in the accuracy metric example.

3. **Implement the metric function**: Create a function that adheres to the protocol defined in the chosen metric registry. Use the appropriate decorator to register your metric function within the A4S evaluation framework.

For example, if you are implementing a model metric, you would use the `@model_metric` decorator:

```pythonpython
from a4s_eval.metric_registries.model_metric_registry import model_metric

@model_metric(name="your_metric_name")
def your_metric_function(
    datashape: DataShape,
    model: Model,
    dataset: Dataset,
    functional_model: FunctionalModel,
) -> list[Measure]:
    # Your metric implementation here
```

4. **Test your metric**: After implementing your metric, it is crucial to test it to ensure it works as expected. You can create unit tests that call your metric function with sample data and models.

A default test suite for model metrics is located in `tests/metrics/model_metrics/test_execute.py`. You can add your metric tests there or create a new test file.

To run the tests, use the following command:

```bash
uv run pytest -s tests/metrics/model_metrics
```

5. **Update the test suite**: If you have added new functionality or modified existing behavior, ensure that your test suite reflects these changes. You may need to duplicate existing test functions and modify them to include your metric.

Something you might want to do is to create tests that evaluate your metric on different datasets, in particular for text generation tasks.

In the case of text generation metrics, you can override the fixtures `textgen_dataset` and `data_shape` (that are functions returning the dataset and data shape respectively) within the `tests/metrics/textgen_metrics/test_execute.py` file.

## About TextGen metrics

Text generation metrics requires an additional dependency on your system.

Follow the intruction to install Ollama [https://ollama.com/download](https://ollama.com/download).

Once installed try running the following command to ensure that Ollama is correctly set up:

```bash
ollama run deepseek-r1:8b
```

This will open a prompt to start interacting with the default model used in the `tests/metrics/textgen_metrics/test_execute` tests.

If for any reason (pertinance of the metric your are implementing, lack of ressources, etc.) you do not want to use the `deepseek-r1:8b` model, you can change the `functional_model` fixture (in.  `tests/metrics/textgen_metrics/test_execute.py`) to use a different model. The list of ollama available models can be found here: [https://ollama.com/models](https://ollama.com/models).

Please note that you will have to download the model you want to use by running `ollama run <model_name>` before executing the tests.
Also, the higher the number of parameters of the model you choose, the more resources  it will require on your system.
