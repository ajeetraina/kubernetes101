# Installing Helm on PWD

## Pre-requisite


```
[node1 install]$ kubectl get nodes
NAME      STATUS     ROLES     AGE       VERSION
node1     Ready      master    2m        v1.11.3node2     Ready      <none>    48s       v1.11.3
node3     NotReady   <none>    32s       v1.11.3
node4     NotReady   <none>    13s       v1.11.3
node5     NotReady   <none>    8s        v1.11.3
```

```
[node1 ~]$ kubectl get nodes -o json |
>       jq ".items[] | {name:.metadata.name} + .status.capacity"

```
```
{
  "name": "node1",
  "cpu": "8",
  "ephemeral-storage": "10Gi",
  "hugepages-1Gi": "0",
  "hugepages-2Mi": "0",
  "memory": "32929612Ki",
  "pods": "110"
}
{
  "name": "node2",
  "cpu": "8",
  "ephemeral-storage": "10Gi",
  "hugepages-1Gi": "0",
  "hugepages-2Mi": "0",
  "memory": "32929612Ki",
  "pods": "110"
}
{
  "name": "node3",
  "cpu": "8",
  "ephemeral-storage": "10Gi",
  "hugepages-1Gi": "0",
  "hugepages-2Mi": "0",
  "memory": "32929612Ki",
  "pods": "110"
}
{
  "name": "node4",
  "cpu": "8",
  "ephemeral-storage": "10Gi",
  "hugepages-1Gi": "0",
  "hugepages-2Mi": "0",
  "memory": "32929612Ki",
  "pods": "110"
}
{
  "name": "node5",
  "cpu": "8",
  "ephemeral-storage": "10Gi",
  "hugepages-1Gi": "0",
  "hugepages-2Mi": "0",
  "memory": "32929612Ki",
  "pods": "110"
}
```

## Installing OpenSSL

```
[node1 ~]$ yum install openssl

```


```
$ curl https://raw.githubusercontent.com/helm/helm/master/scripts/get > get_helm.sh
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```

```
[node1 ~]$ sh get_helm.sh
Downloading https://kubernetes-helm.storage.googleapis.com/helm-v2.11.0-linux-amd64.tar.gz
Preparing to install helm and tiller into /usr/local/bin
helm installed into /usr/local/bin/helm
tiller installed into /usr/local/bin/tiller
get_helm.sh: line 177: which: command not found
Run 'helm init' to configure helm.
```

```
[node1 ~]$ helm init
Creating /root/.helm
Creating /root/.helm/repository
Creating /root/.helm/repository/cache
Creating /root/.helm/repository/local
Creating /root/.helm/plugins
Creating /root/.helm/starters
Creating /root/.helm/cache/archive
Creating /root/.helm/repository/repositories.yaml
Adding stable repo with URL: https://kubernetes-charts.storage.googleapis.com
Adding local repo with URL: http://127.0.0.1:8879/charts
$HELM_HOME has been configured at /root/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.

Please note: by default, Tiller is deployed with an insecure 'allow unauthenticated users' policy.
To prevent this, run `helm init` with the --tiller-tls-verify flag.
For more information on securing your installation see: https://docs.helm.sh/using_helm/#securing-your-helm-installation
Happy Helming
```

