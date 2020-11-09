# Tutorial: Monitoring with Thanos and Nutanix Objects

---
**NOTE**

* Tested with Prometheus release v2.4.3 included with Karbon 2.1.2 & Kubernetes 1.16.13

* Manifest will create `monitoring` namespace object

---

## Requirements

* Nutanix Karbon 2.1.2 or later

* Kubernetes cluster 1.16.13 or later

* [Metrics Server](../metrics-server/README.md)

* Available a Nutanix Objects instance 1.0 or later 

## Create Bucket

1. Connect to Prism Central

2. Open Objects

3. Create an access key

   ![Create bucket](images/01_objects_keys.png)

4. Create a bucket, I called it `thanos`

   ![Create bucket](images/02_objects_bucket.png)

5. Entitle user access

   ![Create bucket](images/03_objects_useraccess.png)
