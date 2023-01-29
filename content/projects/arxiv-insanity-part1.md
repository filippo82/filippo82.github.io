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

Initial static data dump and then daily data loads using arXiv REST APIs.

### Initial static dataset from Kaggle

Initial static dataset from [Kaggle](https://www.kaggle.com/):
[arXiv Dataset](https://www.kaggle.com/datasets/Cornell-University/arxiv)

First, you need to authenticate to use the Kaggle CLI.


Next, download the dataset:

```shell
kaggle datasets download -d Cornell-University/arxiv
unzip ~/Downloads/arxiv.zip
mv ~/Downloads/arxiv-metadata-oai-snapshot.json /YOUR/PROJECT/DATA
rm ~/Downloads/arxiv.zip
```

Or access it directly from GCP... see info on Kaggle.

Load the data into BigQuery.

`dbt`?


#### Prefect

Build a deployment:

```bash
cd pipelines/flows
prefect deployment build ./download_dataset_from_kaggle.py:log_flow -n download_dataset_from_kaggle -q test -sb gcs/block-test -o download_dataset_from_kaggle-deployment.yaml
```

Apply a deployment:

```bash
prefect deployment apply download_dataset_from_kaggle-deployment.yaml
```

### Daily data loads using arXiv REST APIs

TBD

This shall be automated with Prefect.
