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
or short version with selected namespace
``` bash
kubectl get po -n cluster
```
or take a look to yaml
``` bash
kubectl get po -n cluster runner-896858db8-5vhq6 -oyaml
```
or for all namespaces
``` bash
kubectl get po --all-namespaces
```
Expected output:
``` bash
NAMESPACE     NAME                                         READY     STATUS             RESTARTS   AGE
cluster       runner-896858db8-5vhq6                       0/1       ImagePullBackOff   0          1h
docker        compose-7447646cf5-wxm68                     1/1       Running            1          1d
docker        compose-api-6fbc44c575-s4bzx                 1/1       Running            1          1d
kube-system   etcd-docker-for-desktop                      1/1       Running            1          1d
kube-system   kube-apiserver-docker-for-desktop            1/1       Running            1          1d
kube-system   kube-controller-manager-docker-for-desktop   1/1       Running            1          1d
kube-system   kube-dns-86f4d74b45-5ddnp                    3/3       Running            3          1d
kube-system   kube-proxy-vhns5                             1/1       Running            1          1d
kube-system   kube-scheduler-docker-for-desktop            1/1       Running            1          1d
kube-system   tiller-deploy-67d8b477f7-lc592               1/1       Running            0          22h
```

## Get information about a Pod in selected namespace

``` bash
kubectl describe po -n cluster runner-896858db8-tdfgv
```

Expected output:
``` bash
Name:           runner-896858db8-tdfgv
Namespace:      cluster
Node:           docker-for-desktop/192.168.65.3
Start Time:     Tue, 11 Sep 2018 15:06:35 +0300
Labels:         chart=runner-3.5.2
                component=runner
                heritage=Tiller
                pod-template-hash=452414864
                release=runner
                updated=1536661796
Annotations:    <none>
Status:         Running
IP:             10.1.0.8
Controlled By:  ReplicaSet/runner-896858db8
Containers:
...

Events:
  Type     Reason                 Age               From                         Message
  ----     ------                 ----              ----                         -------
  Normal   Scheduled              1m                default-scheduler            Successfully assigned runner-896858db8-tdfgv to docker-for-desktop
  Normal   SuccessfulMountVolume  1m                kubelet, docker-for-desktop  MountVolume.SetUp succeeded for volume "runner-token-5clzz"
  Normal   Pulling                30s (x4 over 1m)  kubelet, docker-for-desktop  pulling image "runner:3.5.2"
  Normal   Pulled                 28s (x4 over 1m)  kubelet, docker-for-desktop  Successfully pulled image "runner:3.5.2"
  Normal   Created                28s (x4 over 1m)  kubelet, docker-for-desktop  Created container
  Normal   Started                28s (x4 over 1m)  kubelet, docker-for-desktop  Started container
  Warning  BackOff                10s (x5 over 1m)  kubelet, docker-for-desktop  Back-off restarting failed container

```

## Delete a Pod

``` bash
kubectl delete po -n cluster runner-896858db8-5vhq6
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

## Get logs from selected namespace

``` bash
kubectl logs -n cluster runner-896858db8-tdfgv
```

Expected output:
``` bash
{"@message":"Init helm","@timestamp":"2018-09-11T12:07:49.987Z","@fields":{"level":"info"}}
{"@message":"start  helm init --upgrade","@timestamp":"2018-09-11T12:07:49.988Z","@fields":{"level":"debug"}}
{"@message":"call   helm init --upgrade","@timestamp":"2018-09-11T12:07:49.989Z","@fields":{"level":"debug"}}
{"@message":"error  helm init --upgrade","@timestamp":"2018-09-11T12:07:50.969Z","@fields":{"level":"error"}}
{"@message":"Error: error when upgrading: current Tiller version is newer, use --force-upgrade to downgrade\n","@timestamp":"2018-09-11T12:07:50.969Z","@fields":{"level":"error"}}
{"@message":"","@timestamp":"2018-09-11T12:07:50.969Z","@fields":{"level":"error"}}
```