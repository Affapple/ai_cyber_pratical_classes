# Environment setup

This document will help you set up your environment to run the practical labs of the course.

## Prerequisites

We assume you are using a Unix-based system (Linux or MacOS). If you are using Windows, we recommend using  WSL (Windows Subsystem for Linux) 2. Learn more about [WSL2 here](https://learn.microsoft.com/en-us/windows/wsl/install).
If you use WSL2, you will have to execute all commands within your WSL2 distribution, not on Windows (cmd.exe or PowerShell).

We assume you have the following tools installed on your system:

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Git Large File Storage (LFS)](https://docs.github.com/en/repositories/working-with-files/managing-large-files/installing-git-large-file-storage)

!!! note
    If you are using Ubuntu, you can install them with:
    ```bash
    sudo apt update
    sudo apt install git git-lfs
    ```

## VSCode

Altough you can use any text editor or IDE, we recommend using [VSCode](https://code.visualstudio.com/) and will provide support for it.
Part of the labs will require you to use Jupyter Notebooks, which are well supported in VSCode.

VSCode is highly customizable and you can install many extensions to improve your productivity.
As a minimum, we recommend installing the following extensions:

- [Python Extension Pack](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python-extension-pack)

To go further, you can read [this article](https://mlops-coding-course.fmind.dev/1.%20Initializing/1.6.%20VS%20Code.html) for more recommendations on VSCode, its extensions and its configurations for Python and Data Science.

## Install uv

We will use 'uv' to manage our Python installation, virtual environments, and dependencies.
Follow the instructions on the [uv installation page](https://docs.astral.sh/uv/getting-started/installation/) to install it on your system.

Verify the installation by running:

```bash
uv --version
```

!!! warning
    UV is package manager just like pip or conda. Do not use pip or conda to install packages in the virtual environments created with uv.
    Use `uv add <package>` to install packages in the current uv environment.

To run a command in a uv environment, you can use `uv run <command>`.
To spawn a shell in the uv environment, you can use `uv shell`.

In the next sections, we will show how to use `uv` and `vscode` to run a Jupyter notebook.

## Connect to GitLab

To clone the repositories, you will need to connect to GitLab using SSH.

First, connect to the University GitLab using your student credentials: [https://gitlab-cloud.uni.lu/](https://gitlab-cloud.uni.lu/).

Then, you will need to generate an SSH key pair and add the public key to your GitLab account.

Follow the instructions on the [GitLab SSH documentation](https://docs.gitlab.com/user/ssh/#see-if-you-have-an-existing-ssh-key-pair).
Start in the linked section "See if you have an existing SSH key pair".

You can leave the passphrase empty if you want, to avoid being prompted for it each time you use the SSH key.

You can skip the section "Configure SSH to point to a different directory".

You can stop at the section "Verify that you can connect".
