# Tutorial: Horizontal Pod Autoscaler

---
**NOTE**

Tested with Metrics Server release v0.4.0 (<https://github.com/kubernetes-sigs/metrics-server/releases/tag/v0.4.0>)

---

## Requirements

* Nutanix Karbon 2.1.2 or later

* Kubernetes cluster 1.16.13 or later

* [Metrics Server](../metrics-server/README.md)

## Create Temporary Namespace

```shell
$ kubectl create namespace karbon-demo-hpa
```

## Create Demo PHP Deployment

```shell
$ kubectl -n karbon-demo-hpa apply -f https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/php-apache.yaml
```

## Create Horizontal Pod Autoscaler

```shell
$ kubectl -n karbon-demo-hpa autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10
```

```shell
$ kubectl -n karbon-demo-hpa get hpa
```

```shell
NAME         REFERENCE               TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   0%/50%    1         10        1          6m3s
```

## Increase load

---
**NOTE**

You'll need two terminals: one for running the test, another for checking the `hpa` object.

---

* Increase load (terminal one):

```shell
$ kubectl -n karbon-demo-hpa run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"
```

* Check load (terminal two) after about a minute:

```shell
$ kubectl -n karbon-demo-hpa get hpa
```

```shell
NAME         REFERENCE               TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   350%/50%   1         10        7          6m35s
```

```shell
$ kubectl -n karbon-demo-hpa get deployment php-apache
```

```shell
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
php-apache   7/7     7            7           13m
```

## Stop load

1. In terminal one cancel the running pod with `<Ctrl> + C`

2. After a minute or more, check the status for hpa:

```shell
$ kubectl -n karbon-demo-hpa get hpa
```

```shell
NAME         REFERENCE               TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   0%/50%    1         10        7          16m
```

## Clean up

```shell
$ kubectl delete namespace karbon-demo-hpa
```

## Credits

* Based on <https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/>
