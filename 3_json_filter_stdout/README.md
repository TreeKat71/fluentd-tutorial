Fluentd tutorial
------------
>Web log [JSON] -> filter (http code:5xx) -> stdout


**Step 1**

You need to write your own `fluentd.conf` with spec below:

1. Collect logs from web application with `in_tail` plugin
2. Web log file is formatted in `JSON` and stored at `/log/web.log`
3. You can tag source as `web.log` or whatever you like
4. Get the server-side error (http code: 5xx) with filter plugin: `grep` 
4. Output to `stdout`


**Step 2**

Create configMap in kubernetes

    $ kubectl create cm fluentd --from-file=fluentd.conf


**Step 3**

Deploy the pod in kubernetes

    $ kubectl apply -f pod.yaml


**Step 4**

    $ kubectl logs apache -c log-collector

If it works properly, you should only see log with 
`status` 5xx

e.g:

    2021-06-30 09:55:30.370567089 +0000 web.log: {"host":"213.135.119.226","user-identifier":"smith6676","datetime":"30/Jun/2021:09:55:28 +0000","method":"PATCH","request":"/world-class/initiatives/content","protocol":"HTTP/1.1","status":500,"bytes":13970,"referer":"http://www.dynamicbricks-and-clicks.net/leverage/monetize/networks/visualize"}
