+++
draft = true
date = 2021-01-30T16:02:36+01:00
updated = 2021-01-30T16:02:36+01:00
title = "Traefik 101"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++


### Resources

* [A Guide to K3s Ingress Using Traefik with NodePort](https://levelup.gitconnected.com/a-guide-to-k3s-ingress-using-traefik-with-nodeport-6eb29add0b4b) as `Tutorial1`
* [Set up Ingress on Minikube with the NGINX Ingress Controller](https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/)
* [Directing Kubernetes traffic with Traefik](https://opensource.com/article/20/3/kubernetes-traefik) as `Tutorial2`


## Tutorial1

kubectl -n kube-system edit cm traefik

[traefikLog]
  format = "json"
[api]
  dashboard = true

kubectl -n kube-system scale deploy traefik --replicas 0
kubectl -n kube-system scale deploy traefik --replicas 1

kubectl -n kube-system port-forward deployment/traefik 8080

http://localhost:8080


wget https://gist.github.com/hyperstripe50/8f47d659c90881c501bffe979576e5a7/raw/222246f0f5236ded55526855b1f74f92791dee01/deployment.yaml

kubectl apply -f ./deployment.yaml

wget https://gist.github.com/hyperstripe50/36eb91b5d8a48b37ad2989feaba4974c/raw/1fa4e6d7adb1f01335af9bbac7cdcda6d6ec8c23/service.yaml

kubectl apply -f ./service.yaml

wget https://gist.github.com/hyperstripe50/839c0657de6e7743409a43fba421bbdb/raw/0147777717a6396ae5239ad540e888537844c939/ingress.yaml

kubectl apply -f ./ingress.yaml


## Tutorial2

wget https://gitlab.com/carpie/ingressing_with_k3s/-/archive/master/ingressing_with_k3s-master.zip




kubectl create configmap mysite-html --from-file index.html

kubectl create configmap mydog-html --from-file html
