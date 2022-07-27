---
title: Kubernetes - RBAC
catalog: true
date: 2022-07-27 22:13:15
subtitle: role & rolebinding clusterrole & clusterrolebinding serviceaccount
header-img:
tags: 
- Cloud
- container
categories:
- TECH
- container
- Kubernetes
---

# Role

## 创建Role

### apply yaml

- `kubectl create role namex —verb=get,watch,list --resource=pods --dry-run=client -o yaml>role1.yaml`
  - 快速获取role1.yaml，再进行修改

- `kubectl apply -f role1.yaml`

### `kubectl create role namex —verb=get,watch,list --resource=pods,deployment`

## 查看Role

### `kubectl get role`

```bash
NAME       AGE
od-reader  7s
```

### `kubectl describe role pod-reader`