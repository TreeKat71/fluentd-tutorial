Setup standalone Minio
------------

<br>

**Install Helm (optional)**

Helm is the package manager for kubernetes and we need it for installing minio.


    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
    chmod 700 get_helm.sh
    ./get_helm.sh


<br>

----

**Step 1**

Add repo and update


    $ helm repo add minio https://operator.min.io/

    $ helm repo update


**Step 2**

Install the minio-operator chart

    $ helm install --namespace minio-operator --create-namespace --generate-name minio/minio-operator

**Step 3**

Creating Minio service

    $ kubectl apply -f s3-tiny.yaml -n fluentd

If you found error, try to create namespace first

    $ kubectl create ns fluentd

<br>

Ref:
    https://github.com/minio/operator/tree/master/helm/minio-operator




