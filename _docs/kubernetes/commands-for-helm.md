---
title: Commands for Helm
category: Kubernetes
order: 2
---

Here are the commands that I've used for Kubernetes before.

## Get chart list

``` bash
helm list
```

Expected output

``` bash
NAME    REVISION        UPDATED                         STATUS          CHART           APP VERSION NAMESPACE
runner  1               Tue Sep 11 13:29:56 2018        DEPLOYED        runner-3.5.2                cluster
```

## Get values from selected chart

``` bash
helm get values runner
```

Expected output

``` bash
app:
  cluster:
    name: some-cluster-name
  configs:
    token: A8McYfWarLL4wXzT
    uri: https://some-uri/svc/staging-configs
  deployments:
    token: A8McYfWarLL4wXzT
    uri: https://some-uri/svc/staging-deployments
  secrets:
    token: A8McYfWarLL4wXzT
    uri: https://some-uri/svc/staging-secrets
image:
  pullSecret: cluster-registry
```