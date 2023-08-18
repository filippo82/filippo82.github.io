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

## Infrastructure

### Docker images

First, we need to create a repository in Google Cloud Artifact Registry.
This should be executed only once:

```shell
GCLOUD_REGION="us-central1"
GCLOUD_ARTIFACTS_REPOSITORY="prefect"
DESCRIPTION="Registry for prefect images"
gcloud artifacts repositories create ${GCLOUD_ARTIFACTS_REPOSITORY} \
    --repository-format=docker \
    --location=${GCLOUD_REGION} \
    --description=${DESCRIPTION} \
    --labels=project=prefect
```

Then we verify that the repository has been actually created:

```shell
gcloud artifacts repositories list --format="json" | jq '.[].name'
```

#### Automated build

Resources:

* [Build and push a Docker image with Cloud Build](https://cloud.google.com/build/docs/build-push-docker-image)
* [Create a build configuration file](https://cloud.google.com/build/docs/configuring-builds/create-basic-configuration)
* [Substituting variable values > Dynamic substitutions](https://cloud.google.com/build/docs/configuring-builds/substitute-variable-values#dynamic_substitutions)

Enable the Cloud Build, Artifact Registry, and Secret Manager APIs using `gcloud`.

Grante the required IAM permissions:

```shell
PN=$(gcloud projects describe ${PROJECT_ID} --format="value(projectNumber)")
CLOUD_BUILD_SERVICE_AGENT="service-${PN}@gcp-sa-cloudbuild.iam.gserviceaccount.com"
gcloud projects add-iam-policy-binding ${PROJECT_ID} \
  --member="serviceAccount:${CLOUD_BUILD_SERVICE_AGENT}" \
  --role="roles/cloudbuild.connectionAdmin"
```

Install the [Google Cloud Build](https://github.com/marketplace/google-cloud-build) app
in your GitHub account.

Set up a GitHub connection and then link a repository from the
[Cloud Build console](https://console.cloud.google.com/cloud-build/repositories/2nd-gen).

Set up a trigger in the right region from the
[Cloud Build console](https://console.cloud.google.com/cloud-build/triggers;region=us-central1).

#### Manual build using Dockerfile

Build your container image using Cloud Build, which is similar to running `docker build` and `docker push`, but the build happens on Google Cloud:

```shell
cd infrastructure/prefect-docker-images/prefect-arxiv-cpu
GCLOUD_PROJECT_ID=$(gcloud config get-value project)
GCLOUD_REGION="us-central1"
GCLOUD_ARTIFACTS_REPOSITORY="prefect"
IMAGE_NAME="prefect-arxiv-cpu"
gcloud builds submit --async \
  --region=${GCLOUD_REGION} \
  --tag "${GCLOUD_REGION}-docker.pkg.dev/${GCLOUD_PROJECT_ID}/${GCLOUD_ARTIFACTS_REPOSITORY}/${IMAGE_NAME}" .
```

> :warning: If you don't set the `--region` flag, this will be a `global` build.

#### Manual build using a build config file

```shell
GCLOUD_REGION="us-central1"
gcloud builds submit \
  --region=${GCLOUD_REGION} \
  --config cloudbuild.yaml
```

> :warning: You need to add `dir` to the build step definition:
> 
> * https://cloud.google.com/build/docs/build-config-file-schema#dir
> * https://stackoverflow.com/a/73474845

## Orchestration

## Prefect

Create a work pool:

```shell
prefect work-pool create "arxiv-normal"
```

## Flows

### `download_dataset_from_kaggle`

Build a deployment:

```shell
cd pipelines/flows/download_dataset_from_kaggle
prefect deployment build ./download_dataset_from_kaggle.py:flow_get_arxiv_kaggle_dataset \
    --name download_dataset_from_kaggle \
    --work-queue arxiv \
    --pool arxiv-normal \
    --storage-block gcs/block-bucket-pipelines \
    --infra-block cloud-run-job/block-cloud-run-job \
    --output download_dataset_from_kaggle-deployment.yaml
```

Apply a deployment:

```shell
prefect deployment apply download_dataset_from_kaggle-deployment.yaml
```

### `compute_embeddings_for_kaggle_dataset`

Build a deployment:

```shell
cd pipelines/flows/compute_embeddings_for_kaggle_dataset
prefect deployment build ./compute_embeddings_for_kaggle_dataset.py:flow_compute_embeddings_for_kaggle_dataset \
    --name compute_embeddings_for_kaggle_dataset \
    --work-queue arxiv \
    --pool arxiv-normal \
    --storage-block gcs/block-bucket-pipelines \
    --infra-block cloud-run-job/block-cloud-run-job \
    --output compute_embeddings_for_kaggle_dataset-deployment.yaml
```

Apply a deployment:

```shell
prefect deployment apply compute_embeddings_for_kaggle_dataset-deployment.yaml
```

### `get_metadata_from_arxiv_api`

Build a deployment:

```shell
cd pipelines/flows/get_metadata_from_arxiv_api
prefect deployment build ./get_metadata_from_arxiv_api.py:flow_get_metadata_from_arxiv_api \
    --name get_metadata_from_arxiv_api \
    --work-queue arxiv \
    --pool arxiv-normal \
    --storage-block gcs/block-bucket-pipelines \
    --infra-block cloud-run-job/block-cloud-run-job \
    --output get_metadata_from_arxiv_api-deployment.yaml
```

Apply a deployment:

```shell
prefect deployment apply get_metadata_from_arxiv_api-deployment.yaml
```

On the VM, we start a Prefect agent:

```shell
prefect agent start -p 'arxiv-normal'
```
