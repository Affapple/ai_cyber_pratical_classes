# Getting started

In this section, we will guide you through the steps to set up your development environment to implement a metric in the `a4s-eval module`.

We assume that you have already completed the environment setup as described in the [Environment Setup](../01-env_setup.md) section and you have completed the [First notebook](../02-first_notebook.md) section.

We also assume you are using a Unix-like operating system (Linux or macOS). If you are using Windows, you may need to adjust some commands accordingly.

## Setting up the environment

First create a directory for your project and navigate into it:

```bash
mkdir a4s
cd a4s
```

Then, clone the `a4s-eval` repository:

```bash
git clone git@gitlab.com:uniluxembourg/snt/serval/teaching/ai-security/a4s-eval.git
cd a4s-eval
```

And install the dependencies using `uv`:

```bash
uv sync
```

This will create a virtual environment in the `.venv` subfolder and install all the dependencies specified in the `pyproject.toml` file.

## Test your environment

To test that your environment is set up correctly, you can run the tests provided in the `a4s-eval` repository.

```bash
uv run pytest
```

If everything is set up correctly, you should see that all tests pass.
This means that you are ready to start implementing your metric!
