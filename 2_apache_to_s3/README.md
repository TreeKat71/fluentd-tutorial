Fluentd tutorial
------------
>Apache -> fluentd -> S3

<br>

**Setup Minio (optional)**

Minio is kinda like a free version of AWS S3.

Please follow the instructions under `infra/minio` folder.

After setting it up, you need to create a bucket called `logs`

<br>

----

**Step 1**

You need to write your own `fluentd.conf` with spec below:

1. Collect logs from apache application with `in_tail` plugin
2. Apache log file is stored at `/log/apache.log`
3. You can tag source as `s3.apache.access` or whatever you like
4. Output to `S3`


**Step 2**

Create configMap in kubernetes

    $ kubectl create cm fluentd --from-file=fluentd.conf


**Step 3**

Deploy the pod in kubernetes

    $ kubectl apply -f pod.yaml


**Step 4**

Check if it does output to the sidecar stout

    $ kubectl logs apache -c log-collector

If it works properly, there should not be any error and you can login minio web to check if the log files landed. (You may need to use port-forwaring or NodePort service to access minio service)


