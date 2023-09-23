# Metrics Server Installation

---
**NOTE**

Tested with Metrics Server release v0.4.0 (<https://github.com/kubernetes-sigs/metrics-server/releases/tag/v0.4.0>)

---

## Requirements

* Nutanix Karbon 2.1.2 or later

* Kubernetes cluster 1.16.13 or later

## Installation

This installs latest Metrics Server release in kube-system namespace:

```console
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

## Configuration

Nutanix Karbon configurations requires:

* `--kubelet-preferred-address-types` set to `InternalIP,ExternalIP,Hostname`

* `--kubelet-insecure-tls`

```console
kubectl -n kube-system patch deployment metrics-server --type='json' -p '[
    {
        "op": "replace",
        "path": "/spec/template/spec/containers/0/args",
        "value": [
            "--cert-dir=/tmp",
            "--secure-port=4443",
            "--kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname",
            "--kubelet-use-node-status-port",
            "--kubelet-insecure-tls"
        ]
    }
]'
```

# Test

To check Metrics Server is working as expected.

* For node metrics:

```console
kubectl top nodes
```

```
NAME                                    CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
karbon-jg-metrics-49f34f-k8s-master-0   116m         5%     2180Mi          65%       
karbon-jg-metrics-49f34f-k8s-worker-0   258m         3%     3935Mi          53%    
```

* For pod metrics:

```console
kubectl top pods
```

```
NAME                                                   CPU(cores)   MEMORY(bytes)   
kube-apiserver-karbon-jg-metrics-49f34f-k8s-master-0   38m          478Mi           
kube-dns-5c64dc6c6b-vflzr                              8m           27Mi            
kube-flannel-ds-2lxnj                                  3m           13Mi            
kube-flannel-ds-7ffwj                                  4m           14Mi            
kube-proxy-ds-76474                                    1m           26Mi            
kube-proxy-ds-7mktq                                    4m           30Mi            
metrics-server-bb4c8fd74-v9wpj                         4m           14Mi      
```
