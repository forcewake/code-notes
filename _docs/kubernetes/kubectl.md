---
title: Commands for Kubernetes
category: Kubernetes
order: 1
---

Here are the commands that I've used for Kubernetes before.

## List all Pods

``` bash
kubectl get pods
```

## List all Services

``` bash
kubectl get services
```

## Create a new Deployment

``` bash
kubectl create -f games.yaml
```

## Delete a Deployment

``` bash
kubectl delete -f games.yaml
```

## Wait for the Status of a Service

``` bash
kubectl get service dont-starve --watch
```

> Useful for the IP address of the service.

## Get the STDOUT STDERR of a pod that is running a Service

``` bash
kubectl logs dont-starve-403593606-zqb6w
```