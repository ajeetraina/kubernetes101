# Building our First nginx Application on k8s cluster

```
[node1 ~]$ kubectl get nodes
NAME      STATUS    ROLES     AGE       VERSION
node1     Ready     master    1h        v1.10.2
node2     Ready     <none>    1h        v1.10.2
node3     Ready     <none>    1h        v1.10.2
node4     Ready     <none>    1h        v1.10.2
node5     Ready     <none>    14m       v1.10.2
[node1 ~]$

```

```
[node1 ~]$ kubectl get po
NAME                     READY     STATUS    RESTARTS   AGE
nginx-5db977d67c-6sdfd   1/1       Running   0          2m
nginx-5db977d67c-jfq9h   1/1       Running   0          2m
nginx-5db977d67c-vs925   1/1       Running   0          2m
nginx-5db977d67c-z5r45   1/1       Running   0          2m
[node1 ~]$

```

## Running Nginx having 4 Replicas

```
kubectl run nginx --image=nginx:latest --replicas=4
```

## Watch the pods

```
kubectl get pods -w
```

## Expose the ElasticSearch HTTP API port:

```

kubectl expose deploy/nginx --port 80

```

## Testing the Nginx Service

```

IP=$(kubectl get svc nginx -o go-template --template '{{ .spec.clusterIP }}')
```

Send a few requests:

```
[node1 ~]$ curl $IP:80
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
[node1 ~]$
```
