---
title: Azure Networking
category: Azure
order: 1
---

## Setup with DNS Service

``` bash
az network dns zone create --resource-group DraftSandbox --name jwendl.net
az network dns zone create --resource-group DraftSandbox --name draft.jwendl.net
az network dns record-set ns create --resource-group DraftSandbox --zone-name jwendl.net --name draft
az network dns record-set ns add-record --resource-group DraftSandbox --zone-name jwendl.net --record-set-name draft --nsdname ns1-03.azure-dns.com.
az network dns record-set ns add-record --resource-group DraftSandbox --zone-name jwendl.net --record-set-name draft --nsdname ns2-03.azure-dns.net.
az network dns record-set ns add-record --resource-group DraftSandbox --zone-name jwendl.net --record-set-name draft --nsdname ns3-03.azure-dns.org.
az network dns record-set ns add-record --resource-group DraftSandbox --zone-name jwendl.net --record-set-name draft --nsdname ns4-03.azure-dns.info.
```