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
My opinionated recommendation is to use [pyenv](https://github.com/pyenv/pyenv).

# `pyenv`

To install it, we use `brew`:

```
brew update
brew install pyenv pyenv-virtualenv
```

Then, we append these lines at the end of the `~/.zshrc` file:

```shell
# pyenv config
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

[pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)

## Usage

First, we list all Python versions available to `pyenv` on the current system:

```shell
pyenv versions
```

Then, we list all available versions:

```shell
pyenv install --list
```
