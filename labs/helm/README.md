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
Loaded plugins: fastestmirror, ovl
base                                                                                                                                        | 3.6 kB  00:00:00
docker-ce-stable                                                                                                                            | 2.9 kB  00:00:00
extras                                                                                                                                      | 3.4 kB  00:00:00
kubernetes/signature                                                                                                                        |  454 B  00:00:00
kubernetes/signature                                                                                                                        | 1.4 kB  00:00:04 !!!
updates                                                                                                                                     | 3.4 kB  00:00:00
(1/6): base/7/x86_64/group_gz                                                                                                               | 166 kB  00:00:00
(2/6): extras/7/x86_64/primary_db                                                                                                           | 204 kB  00:00:00
(3/6): base/7/x86_64/primary_db                                                                                                             | 5.9 MB  00:00:00
(4/6): updates/7/x86_64/primary_db                                                                                                          | 6.0 MB  00:00:00
(5/6): docker-ce-stable/x86_64/primary_db                                                                                                   |  17 kB  00:00:00
(6/6): kubernetes/primary                                                                                                                   |  37 kB  00:00:00
Determining fastest mirrors
 * base: mirror.seedvps.com
 * extras: ams.edge.kernel.org
 * updates: ams.edge.kernel.org
kubernetes                                                                                                                                                 272/272
Resolving Dependencies
--> Running transaction check
---> Package openssl.x86_64 1:1.0.2k-12.el7 will be installed
--> Processing Dependency: openssl-libs(x86-64) = 1:1.0.2k-12.el7 for package: 1:openssl-1.0.2k-12.el7.x86_64
--> Processing Dependency: make for package: 1:openssl-1.0.2k-12.el7.x86_64
--> Running transaction check
---> Package make.x86_64 1:3.82-23.el7 will be installed
---> Package openssl-libs.x86_64 1:1.0.2k-8.el7 will be updated
---> Package openssl-libs.x86_64 1:1.0.2k-12.el7 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

===================================================================================================================================================================
 Package                                  Arch                               Version                                        Repository                        Size
===================================================================================================================================================================
Installing:
 openssl                                  x86_64                             1:1.0.2k-12.el7                                base                             492 k
Installing for dependencies:
 make                                     x86_64                             1:3.82-23.el7                                  base                             420 k
Updating for dependencies:
 openssl-libs                             x86_64                             1:1.0.2k-12.el7                                base                             1.2 M

Transaction Summary
===================================================================================================================================================================
Install  1 Package  (+1 Dependent package)
Upgrade             ( 1 Dependent package)

Total download size: 2.1 M
Is this ok [y/d/N]: y
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/3): make-3.82-23.el7.x86_64.rpm                                                                                                          | 420 kB  00:00:00
(2/3): openssl-1.0.2k-12.el7.x86_64.rpm                                                                                                     | 492 kB  00:00:00
(3/3): openssl-libs-1.0.2k-12.el7.x86_64.rpm                                                                                                | 1.2 MB  00:00:00
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                              9.5 MB/s | 2.1 MB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Updating   : 1:openssl-libs-1.0.2k-12.el7.x86_64                                                                                                             1/4
  Installing : 1:make-3.82-23.el7.x86_64                                                                                                                       2/4
  Installing : 1:openssl-1.0.2k-12.el7.x86_64                                                                                                                  3/4
  Cleanup    : 1:openssl-libs-1.0.2k-8.el7.x86_64                                                                                                              4/4
  Verifying  : 1:make-3.82-23.el7.x86_64                                                                                                                       1/4
  Verifying  : 1:openssl-1.0.2k-12.el7.x86_64                                                                                                                  2/4
  Verifying  : 1:openssl-libs-1.0.2k-12.el7.x86_64                                                                                                             3/4
  Verifying  : 1:openssl-libs-1.0.2k-8.el7.x86_64                                                                                                              4/4

Installed:
  openssl.x86_64 1:1.0.2k-12.el7

Dependency Installed:
  make.x86_64 1:3.82-23.el7

Dependency Updated:
  openssl-libs.x86_64 1:1.0.2k-12.el7

Complete!

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

