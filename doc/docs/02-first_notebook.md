# First Jupyter Notebook

In this section, we will show you how to run a Jupyter notebook using `uv` and `vscode`.

We will use the notebook `1_first_notebook.ipynb` as an example.

## Cloning the repository

First, clone this repository to your local machine:

```bash
git clone INSERT_REPO_URL_HERE
cd course-ai-security
```

In the `src` folder, you will find a folder for each labs in this course.

For the first lab, navigate to the `01_environment_setup` folder:

```bash
cd src/01_environment_setup
```

## Creating the environment

In previous sections, we installed `uv` to manage our environments.
Each labs has its own environment with different python versions and dependencies.
The python version is defined in the `.python-version` file, while the dependencies are defined in the `pyproject.toml` file.

To create the environment for this lab, run the following command:

```bash
uv sync
```

This command will read the `.python-version` and `pyproject.toml` files, install the python versions if needed, create a virtual environment (in the `.venv` subfolder) with the specified python version and dependencies.

## Using the environment in vscode

Once the environment is created, you can activate it in vscode.
To do so, open the labs folder in vscode:

```bash
code .
```

Then, open the command palette (Ctrl+Shift+P) and search for `Python: Select Interpreter`.
Select the interpreter located in the `.venv` folder.
For the first lab, it should be something like `Python 3.8.10 (01-environment-setup) ./.venv/bin/python)`.

Once the interpreter is selected, you can open the notebook `01_environment_setup.ipynb` and start running the cells.
