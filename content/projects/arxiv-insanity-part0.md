+++
draft = false
date = 2023-01-07T20:19:33+01:00
updated = 2023-01-08T20:19:33+01:00
title = "arXiv insanity - Part 0 - Setup all the things!"
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

## Set up the Compute Engine instance

When setting up a virtual machine, I choose Ubuntu 22.04.2 LTS as the operative system.

First, I install a set of packages which are required by `pyenv` for building Python:

```shell
sudo apt update
sudo apt --assume-yes install build-essential libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev curl \
    libncursesw5-dev xz-utils tk-dev libxml2-dev \
    libxmlsec1-dev libffi-dev liblzma-dev
```

Install `pyenv` with the [`pyenv` installer](https://github.com/pyenv/pyenv-installer):

```shell
curl https://pyenv.run | bash
```

Then, add the following lines to `~/.bashrc`:

```shell
# See https://github.com/pyenv/pyenv/issues/2417#issuecomment-1257017013
[[ -d $HOME/.local/bin && :$PATH: != *":$HOME/.local/bin:"* ]] && export PATH="$HOME/.local/bin:$PATH"

# pyenv
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

Finally, restart your shell for the changes to take effect.

For this project, I use `pyenv` to install a recent version of Python 3.11:

```shell
pyenv install 3.11.4
pyenv global 3.11.4
```

On a small virtual machine, installing a new Python version will take up to one hour.

{{< notice warning >}}

Potential issues:

https://github.com/pyenv/pyenv/issues/2417#issuecomment-1257017013

{{< /notice >}}

## Clone repository

```shell
# git clone git@github.com:filippo82/arxiv-insanity.git
git clone https://github.com/filippo82/arxiv-insanity.git
```

{{< notice tip >}}

Make sure you are authorised to clone a repo from the current environment.
You might need to follow [these instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

{{< /notice >}}

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

{{< notice warning >}}

You might need to add the `--no-cache-dir` flag when installing `torch`.

{{< /notice >}}

ADD BOX

Add link to blog post with my opinionated Python setup.

## Credentials

* Google Cloud
* Kaggle
* Prefect Cloud

### Google Cloud

First install the Google Cloud CLI by following the [official instructions](https://cloud.google.com/sdk/docs/install#mac). If already installed, you can update its components to the latest version:

```shell
sudo apt-get install apt-transport-https ca-certificates gnupg curl sudo
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
sudo apt-get update && sudo apt-get --assume-yes install google-cloud-cli
gcloud components update
```

Finally, you can authenticate yourself with `gcloud`:

```shell
gcloud auth login
gcloud projects list
gcloud config set project algebraic-fin-232107
gcloud auth application-default login
```

### Kaggle

To use the Kaggle CLI,
follow these [instructions](https://www.kaggle.com/docs/api#getting-started-installation-&-authentication):

* go to your [account](https://www.kaggle.com/YOUR_USERNAME/account) on Kaggle;
* generate a new API token;
* move the downloaded `kaggle.json` file to `~/.kaggle/kaggle.json`;
* run `chmod 600 ~/.kaggle/kaggle.json` to ensure that `kaggle.json` has the right permissions.

### Prefect Cloud

TBD

```shell
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
