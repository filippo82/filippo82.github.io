+++
draft = true
date = 2023-01-07T20:19:33+01:00
updated = 2023-01-08T20:19:33+01:00
title = "arXiv insanity - Part 0 - Setup"
description = ""
slug = ""
tags = []
categories = []
externalLink = ""
series = [
    "App"
]
+++

<span class="firstcharacter">S</span>etup!

## Introduction

TBD

## Set up VM

```bash
sudo apt install python3.10-venv
```

```bash
python3 -m venv venvs/arxiv
source venvs/arxiv/bin/activate
```

## Clone repository

```bash
git clone git@github.com:filippo82/arxiv-insanity.git
```

ADD BOX

Make sure you are authorised to clone a repo from the current environment.
You might need to follow [these instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

## Python environment

TBD

```shell
cd arxiv-insanity
pyenv virtualenv arxiv
pyenv local arxiv
pip install -U -r requirements.txt
pip install -U -r requirements-dev.txt
pre-commit install
```

## Credentials

### Kaggle

To use the Kaggle CLI,
follow these [instructions](https://www.kaggle.com/docs/api#getting-started-installation-&-authentication):

* go to your [account](https://www.kaggle.com/YOUR_USERNAME/account) on Kaggle;
* generate a new API token;
* move the downloaded `kaggle.json` file to `~/.kaggle/kaggle.json`;
* run `chmod 600 ~/.kaggle/kaggle.json` to ensure that `kaggle.json` has the right permissions.

### Prefect Cloud

TBD

```bash
prefect cloud login --key xxx_XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX --workspace "your_handle/your_workspace"
```

ADD BOX

If you have not created a workspace yet, you will be asked to create one
when logging in for the first time with `prefect cloud login`.


In your local environment, where you executed the login command above,
create a file named `basic_flow.py` with the following contents:

```python
from prefect import flow, get_run_logger

@flow(name="Testing")
def basic_flow():
    logger = get_run_logger()
    logger.warning("The fun is about to begin")

if __name__ == "__main__":
    basic_flow()
```

Now run `python basic_flow.py`.
Go to the dashboard for your workspace in Prefect Cloud.
You'll see the flow run results in the `Flow Runs` panel.
