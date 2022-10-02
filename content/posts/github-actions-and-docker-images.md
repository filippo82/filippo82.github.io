+++ 
draft = true
date = 2022-09-10T01:04:34+02:00
updated = 2022-09-10T01:04:34+02:00
title = "Build and push Docker images with GitHub actions"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Create a new GitHub repository. I named mine [`docker-images`](https://github.com/filippo82/docker-images).

First, go to [hub.docker.com](https://hub.docker.com) and log in.
Then, click on your user name in the top right and then on Account Settings.
Select the Security tab on the left and create a new access token by clicking on the button.
Choose a meaningful name for the token and then select Read & Write permissions.
Copy the token and add it as a secret in the Settings -> Secrets -> Actions
of your GitHub repository.



Add the `build-and-publish.yaml` file to `.github/workflows` directory.

References:

* https://github.com/docker/build-push-action/
* https://event-driven.io/en/how_to_buid_and_push_docker_image_with_github_actions/
* https://docs.docker.com/ci-cd/github-actions/
