
Fluentd tutorial
------------
>Apache -> fluentd -> stdout

**Step 1**

You need to write your own `fluentd.conf` with spec below:

1. Collect logs from apache application with `in_tail` plugin
2. Apache log file is stored at `/log/apache.log`
3. You can tag source as `apache.access` or whatever you like
4. Output to stdout


**Step 2**

Create configMap in kubernetes

    $ kubectl create cm fluentd --from-file=fluentd.conf


**Step 3**

Deploy the pod in kubernetes

    $ kubectl apply -f pod.yaml


**Step 4**

Check if it does output to the sidecar stout

    $ kubectl logs apache -c log-collector

If it works properly, you should see some json formatted string line by line.

    2021-06-28 21:03:58.000000000 +0000 apache.access: {"host":"122.76.61.134","user":null,"method":"POST","path":"/architect","code":504,"size":56501,"referer":"https://www.globalcross-media.io/rich/relationships","agent":"Mozilla/5.0 (X11; Linux i686) AppleWebKit/5360 (KHTML, like Gecko) Chrome/36.0.810.0 Mobile Safari/5360"}

