+++ 
draft = false
date = 2022-09-05T23:18:20+02:00
updated = 2022-10-01T23:18:20+02:00
title = "How to set up python on your computer"
description = ""
slug = ""
authors = ["Filippo"]
tags = [
    "development"
]
categories = []
externalLink = ""
series = [
    "Development"
]
+++

<span class="firstcharacter">T</span>here are many ways to install Python.
You can ask three people about this topic and you will get five different opinions.
My opinionated recommendation is to use [pyenv](https://github.com/pyenv/pyenv)
to install and manage multiple Python versions
and its companion [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
to manage virtual environments.

If you are a macOS user like me,
you should use [Homebrew](https://brew.sh/) to install it.

```shell
brew update
brew install pyenv pyenv-virtualenv
```

{{< notice tip >}}

If you have not used Homebrew yet, you can install it with this command:

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

{{< /notice >}}

Then, we append these lines at the end of the `~/.zshrc` file:

```shell
# pyenv config
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

## Usage

First, we list all Python versions available to `pyenv` on the current system:

```shell
pyenv versions
```

Then, we list all available versions:

```shell
pyenv install --list
```

To create a virtual environment, you can execute a similar command:

```shell
pyenv virtualenv 3.11.4 arxiv-3.11.4
```

This will create a virtualenv based on Python 3.11.4 under `$(pyenv root)/versions`
in a folder called `arxiv-3.11.4`.

If you want to automatically activate a specific virtual environment once you access
a specific directory, you can execute `pyenv local arxiv-3.11.4` inside that directory.
This will create a `.python-version` which indicates the virtual environment to activate.
