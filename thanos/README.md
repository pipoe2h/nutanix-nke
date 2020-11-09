# Tutorial: Monitoring with Prometheus, Thanos and Nutanix Objects

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

## Create Objects Secret

In this step you will create a Kubernetes secret with the configuration for Objects. You will need:

* The keys you created in the previous section

* Bucket name

* Objects URL

In the folder along with the other YAML files create the following file replacing the `bucket`, `endpoint`, `access_key` and `secret_key` with yours. This file will be used with Kubernetes Kustomize later

    ```shell
    cat <<EOF >./objects.properties
    type: s3
    config:
      region: us-east-1
      bucket: YOUR_BUCKET_NAME_HERE
      endpoint: YOUR_ENDPOINT_URL_HERE
      access_key: YOUR_ACCESS_KEY_HERE
      secret_key: YOUR_SECRET_KEY_HERE
      http_config:
        insecure_skip_verify: true
    EOF
    ```
