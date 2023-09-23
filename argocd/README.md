# Argo CD Installation

---
**NOTE**

Tested with Argo CD release v2.8.4 (<https://github.com/argoproj/argo-cd/releases/tag/v2.8.4>)

---

## Requirements

* Nutanix Kubernetes Engine 2.8 or later

* Kubernetes cluster 1.25.6 or later

## Installation

This installs Argo CD 2.8.4 release in argocd namespace:

```console
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.8.4/manifests/ha/install.yaml
```
