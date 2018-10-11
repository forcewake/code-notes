---
title: Commands for Kubernetes
category: Kubernetes
order: 1
---

Here are the commands that I've used for Kubernetes before.

Some of them are from [this gist](https://gist.github.com/edsiper/fac9a816898e16fc0036f5508320e8b4#volumes)

Helper setup to edit .yaml files with Vim:

- [VIM Setup for Yaml files](#vim-setup-for-yaml-files)

List of general purpose commands for Kubernetes management:

- [PODS](#pods)
- [Create Deployments](#create-deployments)
- [Scaling PODs](#scaling-pods)
- [POD Upgrade / History](#pod-upgrade-and-history)
- [Services](#services)
- [Volumes](#volumes)
- [Secrets](#secrets)
- [ConfigMaps](#configmaps)
- [Ingress](#ingress)
- [Horizontal Pod Autoscalers](#horizontal-pod-autoscalers)
- [Scheduler](#scheduler)
- [Taints and Tolerations](#tains_and_tolerations)
- [Troubleshooting](#troubleshooting)
- [Role Based Access Control (RBAC)](#role_based_access_control)
- [Security Contexts](#security_contexts)
- [Pod Security Policies](#pod_security_policies)
- [Network Policies](#network_policies)

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

## Use infrastructure services outside the cluster

If you want to use some service from outside the cluster (for example, postgres or redis for local development) consider using k8s [port-forwarding](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/). For example, redis from local k8s cluster can be exposed like:
```
 kubectl port-forward svc/redis-master-svc -n redis 6379:6379
```

## VIM Setup for Yaml files

Put the following lines in ~/.vimrc:

```
" Yaml file handling
autocmd FileType yaml setlocal ts=2 sts=2 sw=2 expandtab
filetype plugin indent on
autocmd FileType yaml setl indentkeys-=<:>

" Copy paste with ctr+c, ctr+v, etc
:behave mswin
:set clipboard=unnamedplus
:smap <Del> <C-g>"_d
:smap <C-c> <C-g>y
:smap <C-x> <C-g>x
:imap <C-v> <Esc>pi
:smap <C-v> <C-g>p
:smap <Tab> <C-g>1> 
:smap <S-Tab> <C-g>1<
```

Keyboard hints:

- ctrl + f: auto indent line (requires INSERT mode)

## PODS

```
$ kubectl get pods
$ kubectl get pods --all-namespaces
$ kubectl get pod monkey -o wide
$ kubectl get pod monkey -o yaml
$ kubectl describe pod monkey
```

## Create Deployments

Create single deployment

```
$ kubectl run monkey --image=monkey --record
```

## Scaling PODs

```bash
$ kubectl scale deployment/POD_NAME --replicas=N
```

## POD Upgrade and history

#### List history of deployments

```
$ kubectl rollout history deployment/DEPLOYMENT_NAME
```

#### Jump to specific revision

```
$ kubectl rollout undo deployment/DEPLOYMENT_NAME --to-revision=N
```

## Services

List services

```
$ kubectl get services
```

Expose PODs as services (creates endpoints)

```
$ kubectl expose deployment/monkey --port=2001 --type=NodePort
```

## Volumes

Lits Persistent Volumes and Persistent Volumes Claims:

```
$ kubectl get pv
$ kubectl get pvc
```

## Secrets

```
$ kubectl get secrets
$ kubectl create secret generic --help
$ kubectl create secret generic mysql --from-literal=password=root
$ kubectl get secrets mysql -o yaml
```
## ConfigMaps

```
$ kubectl create configmap foobar --from-file=config.js
$ kubectl get configmap foobar -o yaml
```

## DNS

List DNS-PODs:

```
$ kubectl get pods --all-namespaces |grep dns
```

Check DNS for pod nginx (assuming a busybox POD/container is running)

```
$ kubectl exec -ti busybox -- nslookup nginx
```

> Note: kube-proxy running in the worker nodes manage services and set iptables rules to direct traffic.

## Ingress

Commands to manage Ingress for ClusterIP service type:

```
$ kubectl get ingress
$ kubectl expose deployment ghost --port=2368
```

Spec for ingress:

- [backend](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx)
 
## Horizontal Pod Autoscaler

When heapster runs:

```
$ kubectl get hpa
$ kubectl autoscale --help
```

## DaemonSets

```
$ kubectl get daemonsets
$ kubectl get ds
```

## Scheduler

NodeSelector based policy:

```
$ kubectl label node minikube foo=bar
```

Node Binding through API Server:

```
$ kubectl proxy 
$ curl -H "Content-Type: application/json" -X POST --data @binding.json http://localhost:8001/api/v1/namespaces/default/pods/foobar-sched/binding
```

## Tains and Tolerations

```
$ kubectl taint node master foo=bar:NoSchedule
```

## Troubleshooting

```
$ kubectl describe
$ kubectl logs
$ kubectl exec
$ kubectl get nodes --show-labels
$ kubectl get events
```

Docs Cluster: 
- https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/
- https://github.com/kubernetes/kubernetes/wiki/Debugging-FAQ

## Role Based Access Control

- Role
- ClusterRule
- Binding
- ClusterRoleBinding

```
$ kubectl create role fluent-reader --verb=get --verb=list --verb=watch --resource=pods
$ kubectl create rolebinding foo --role=fluent-reader --user=minikube
$ kubectl get rolebinding foo -o yaml
```

## Security Contexts

Docs: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/

- spec
 - securityCOntext
   - runAsNonRoot: true
   
## Pod Security Policies

Docs: https://github.com/kubernetes/kubernetes/blob/master/examples/podsecuritypolicy/rbac/README.md

## Network Policies

Network isolation at Pod level by using annotations

```
$ kubectl annotate ns <namespace> "net.beta.kubernetes.io/network-policy={\"ingress\": {\"isolation\": \"DefaultDeny\"}}"
```

More about Network Policies as a resource: 

https://kubernetes.io/docs/tasks/administer-cluster/declare-network-policy/