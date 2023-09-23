# Tutorial: Kubernetes Dashboard

---
**NOTE**

* Tested with Metrics Server release v0.4.0 (<https://github.com/kubernetes-sigs/metrics-server/releases/tag/v0.4.0>)

* Tested with Kubernetes Dashboard release v2.0.0 (<https://github.com/kubernetes/dashboard/releases/tag/v2.0.0>)

* Manifest will create `kubernetes-dashboard` namespace object

---

## Recommendations

1. If you'd like to see the metrics in Kubernetes Dashboard, you'll have to install [Metrics Server](../metrics-server/README.md)

## Deploying the Dashboard UI

```console
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

## Accessing the Dashboard UI

```console
kubectl proxy
```

The dashboard is available at <http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/>

## Clean up

```console
kubectl delete -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

## Credits

* Based on <https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/>
