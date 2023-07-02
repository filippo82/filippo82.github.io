+++ 
draft = true
date = 2022-08-31T17:10:35+02:00
updated = 2022-08-31T17:10:35+02:00
title = "Prefect 101"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = [
    
]
+++

<span class="firstcharacter">H</span>owdy folks!
I believe that Prefect documentation a bit too confusing. I find it difficult to digest its concepts.
For this reason, I wrote this post to demystify Prefect!

```shell
python -m venv venvs/prefect
source venvs/prefect/bin/activate
pip install -U prefect
prefect version
```

Where the `requirements.txt` file has this content:

```shell
prefect
```

## GCP

### APIs

Enable

* Cloud Run Admin API
  * https://console.developers.google.com/apis/api/run.googleapis.com/overview?project=404953911638

### Access Scopes for the VM

* Cloud Platform
* Storage

### Permissions

https://cloud.google.com/artifact-registry/docs/access-control#compute


https://cloud.google.com/artifact-registry/docs/docker/authentication

sudo usermod -a -G docker ${USER}

gcloud auth configure-docker us-central1-docker.pkg.dev

Note: If you normally run Docker commands on Linux with sudo, Docker looks for Artifact Registry credentials in /root/.docker/config.json instead of $HOME/.docker/config.json. If you want to use sudo with docker commands instead of using the Docker security group, configure credentials with sudo gcloud auth configure-docker instead.

### Set up the VM

```shell
sudo apt-get update
sudo apt-get install python3-pip docker.io docker-credential-gcr
```

Install `pyenv`:

```shell
sudo apt-get install make build-essential zlib1g-dev libssl-dev liblzma-dev libncurses5-dev libsqlite3-dev libreadline-dev libbz2-dev libffi-dev
curl https://pyenv.run | bash
```

Follow the instructions and add this bit to `~/.bashrc`:

```shell
TBD
```

Install a python version and set it as `global`:

```shell
pyenv install 3.10.11
pyenv global 3.10.11
```

Intall `pyenv-virtualenv`:

```shell
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
```

## Prefect concepts

### Blocks

List existing blocks:

```bash
prefect block ls
```

### Deployments

Build a deployment:

```bash
prefect deployment build ./log_flow.py:log_flow -n log-flow-gcs-cloud-run -q test -sb gcs/block-test -ib cloud-run-job/block-cloud-run-job -o log-flow-gcs-cloud-run-deployment.yaml
```

Apply a deployment:

```bash
prefect deployment apply log-flow-gcs-cloud-run-deployment.yaml
```

## Tutorial

### Docker image

```bash
docker build . -t us-central1-docker.pkg.dev/algebraic-fin-232107/prefect/prefect-test
```

```bash
docker push us-central1-docker.pkg.dev/algebraic-fin-232107/prefect/prefect-test
```
