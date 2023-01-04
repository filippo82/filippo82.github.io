+++
draft = true
date = 2022-12-08T20:19:33+01:00
updated = 2022-02-08T20:19:33+01:00
title = "arXiv insanity - Part 1"
description = ""
slug = ""
tags = []
categories = []
externalLink = ""
series = [
    "App"
]
+++

<span class="firstcharacter">H</span>owdy folks!

## Introduction

TBD

## Data

TBD

Initial static dataset from [Kaggle](https://www.kaggle.com/):
[arXiv Dataset](https://www.kaggle.com/datasets/Cornell-University/arxiv)

First, you need to authenticate to use the Kaggle CLI.
To do so, follow the [instructions](https://www.kaggle.com/docs/api#getting-started-installation-&-authentication):

* go to your [account](https://www.kaggle.com/YOUR_USERNAME/account) on Kaggle;
* generate a new API token;
* move the downloaded `kaggle.json` file to `~/.kaggle/kaggle.json`;
* run `chmod 600 ~/.kaggle/kaggle.json` to ensure that `kaggle.json` has the right permissions.

Next, download the dataset:

```shell
kaggle datasets download -d Cornell-University/arxiv
unzip ~/Downloads/arxiv.zip
mv ~/Downloads/arxiv-metadata-oai-snapshot.json /YOUR/PROJECT/DATA
rm ~/Downloads/arxiv.zip
```



