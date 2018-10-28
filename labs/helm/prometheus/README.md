# Installing Prometheus using Helm

```
[node1 ~]$ helm search prometheus
NAME                                    CHART VERSION   APP VERSION     DESCRIPTION
stable/prometheus                       7.3.4           2.4.3           Prometheus is a monitoring system and time series database.
stable/prometheus-adapter               v0.2.0          v0.2.1          A Helm chart for k8s prometheus adapter
stable/prometheus-blackbox-exporter     0.1.3           0.12.0          Prometheus Blackbox Exporter
stable/prometheus-cloudwatch-exporter   0.2.1           0.5.0           A Helm chart for prometheus cloudwatch-exporter
stable/prometheus-couchdb-exporter      0.1.0           1.0             A Helm chart to export the metrics from couchdb in Promet...
stable/prometheus-mysql-exporter        0.2.1           v0.11.0         A Helm chart for prometheus mysql exporter with cloudsqlp...
stable/prometheus-node-exporter         0.5.0           0.16.0          A Helm chart for prometheus node-exporter
stable/prometheus-operator              0.1.7           0.24.0          Provides easy monitoring definitions for Kubernetes servi...
stable/prometheus-postgres-exporter     0.5.0           0.4.6           A Helm chart for prometheus postgres-exporter
stable/prometheus-pushgateway           0.1.3           0.6.0           A Helm chart for prometheus pushgateway
stable/prometheus-rabbitmq-exporter     0.1.4           v0.28.0         Rabbitmq metrics exporter for prometheus
stable/prometheus-redis-exporter        0.3.2           0.21.1          Prometheus exporter for Redis metrics
stable/prometheus-to-sd                 0.1.1           0.2.2           Scrape metrics stored in prometheus format and push them ...
stable/elasticsearch-exporter           0.4.0           1.0.2           Elasticsearch stats exporter for Prometheus
stable/karma                            1.1.2           v0.14           A Helm chart for Karma - an UI for Prometheus Alertmanager
stable/stackdriver-exporter             0.0.4           0.5.1           Stackdriver exporter for Prometheus
stable/weave-cloud                      0.3.0           1.1.0           Weave Cloud is a add-on to Kubernetes which provides Cont...
stable/kube-state-metrics               0.9.0           1.4.0           Install kube-state-metrics to generate and expose cluster...
stable/mariadb                          5.2.2           10.1.36         Fast, reliable, scalable, and easy to use open-source rel...
[node1 ~]$
```

## Update the Repo

```
[node1 ~]$ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈ Happy Helming!⎈
```

## Installing Prometheus

```
$helm install stable/prometheus
```

Error:
namespaces "default" is forbidden: User "system:serviceaccount:kube-system:default" cannot get namespaces in the namespace "default"


## How to fix?

```
kubectl create serviceaccount --namespace kube-system tiller
```

```
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
```

```
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}' 
```

## Listing Helm

```
[node1 ~]$ helm list
NAME            REVISION        UPDATED                         STATUS          CHART                   APP VERSION     NAMESPACE
excited-elk     1               Sun Oct 28 10:00:02 2018        DEPLOYED        prometheus-7.3.4        2.4.3           default
```

```
[node1 ~]$ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈ Happy Helming!⎈
[node1 ~]$ helm install stable/prometheus
NAME:   excited-elk
LAST DEPLOYED: Sun Oct 28 10:00:02 2018
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1beta1/DaemonSet
NAME                                  AGE
excited-elk-prometheus-node-exporter  1s

==> v1/Pod(related)

NAME                                                        READY  STATUS             RESTARTS  AGE
excited-elk-prometheus-node-exporter-7bjqc                  0/1    ContainerCreating  0         1s
excited-elk-prometheus-node-exporter-gbcd7                  0/1    ContainerCreating  0         1s
excited-elk-prometheus-node-exporter-tk56q                  0/1    ContainerCreating  0         1s
excited-elk-prometheus-node-exporter-tkk9b                  0/1    ContainerCreating  0         1s
excited-elk-prometheus-alertmanager-68f4f57c97-wrfjz        0/2    Pending            0         1s
excited-elk-prometheus-kube-state-metrics-858d44dfdc-vt4wj  0/1    ContainerCreating  0         1s
excited-elk-prometheus-pushgateway-58bfd54d6d-m4n69         0/1    ContainerCreating  0         1s
excited-elk-prometheus-server-5958586794-b97xn              0/2    Pending            0         1s

==> v1/ConfigMap

NAME                                 AGE
excited-elk-prometheus-alertmanager  1s
excited-elk-prometheus-server        1s

==> v1/ServiceAccount
excited-elk-prometheus-alertmanager        1s
excited-elk-prometheus-kube-state-metrics  1s
excited-elk-prometheus-node-exporter       1s
excited-elk-prometheus-pushgateway         1s
excited-elk-prometheus-server              1s

==> v1beta1/ClusterRole
excited-elk-prometheus-kube-state-metrics  1s
excited-elk-prometheus-server              1s

==> v1beta1/Deployment
excited-elk-prometheus-alertmanager        1s
excited-elk-prometheus-kube-state-metrics  1s
excited-elk-prometheus-pushgateway         1s
excited-elk-prometheus-server              1s

==> v1/PersistentVolumeClaim
excited-elk-prometheus-alertmanager  1s
excited-elk-prometheus-server        1s

==> v1beta1/ClusterRoleBinding
excited-elk-prometheus-kube-state-metrics  1s
excited-elk-prometheus-server              1s

==> v1/Service
excited-elk-prometheus-alertmanager        1s
excited-elk-prometheus-kube-state-metrics  1s
excited-elk-prometheus-node-exporter       1s
excited-elk-prometheus-pushgateway         1s
excited-elk-prometheus-server              1s


NOTES:
The Prometheus server can be accessed via port 80 on the following DNS name from within your cluster:
excited-elk-prometheus-server.default.svc.cluster.local


Get the Prometheus server URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9090


The Prometheus alertmanager can be accessed via port 80 on the following DNS name from within your cluster:
excited-elk-prometheus-alertmanager.default.svc.cluster.local


Get the Alertmanager URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=alertmanager" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9093


The Prometheus PushGateway can be accessed via port 9091 on the following DNS name from within your cluster:
excited-elk-prometheus-pushgateway.default.svc.cluster.local


Get the PushGateway URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9091

For more information on running Prometheus, visit:
https://prometheus.io/
```

```
[node1 ~]$ kubectl get all
NAME                                                             READY     STATUS    RESTARTS   AGE
pod/excited-elk-prometheus-alertmanager-68f4f57c97-wrfjz         0/2       Pending   0          3m
pod/excited-elk-prometheus-kube-state-metrics-858d44dfdc-vt4wj   1/1       Running   0          3m
pod/excited-elk-prometheus-node-exporter-7bjqc                   1/1       Running   0          3m
pod/excited-elk-prometheus-node-exporter-gbcd7                   1/1       Running   0          3m
pod/excited-elk-prometheus-node-exporter-tk56q                   1/1       Running   0          3m
pod/excited-elk-prometheus-node-exporter-tkk9b                   1/1       Running   0          3m
pod/excited-elk-prometheus-pushgateway-58bfd54d6d-m4n69          1/1       Running   0          3m
pod/excited-elk-prometheus-server-5958586794-b97xn               0/2       Pending   0          3m

NAME                                                TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
service/excited-elk-prometheus-alertmanager         ClusterIP   10.106.159.46   <none>        80/TCP     3m
service/excited-elk-prometheus-kube-state-metrics   ClusterIP   None            <none>        80/TCP     3m
service/excited-elk-prometheus-node-exporter        ClusterIP   None            <none>        9100/TCP   3m
service/excited-elk-prometheus-pushgateway          ClusterIP   10.106.88.15    <none>        9091/TCP   3m
service/excited-elk-prometheus-server               ClusterIP   10.107.15.64    <none>        80/TCP     3m
service/kubernetes                                  ClusterIP   10.96.0.1       <none>        443/TCP    37m

NAME                                                  DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/excited-elk-prometheus-node-exporter   4         4         4         4            4           <none>          3m

NAME                                                        DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/excited-elk-prometheus-alertmanager         1         1         1            0           3m
deployment.apps/excited-elk-prometheus-kube-state-metrics   1         1         1            1           3m
deployment.apps/excited-elk-prometheus-pushgateway          1         1         1            1           3m
deployment.apps/excited-elk-prometheus-server               1         1         1            0           3m

NAME                                                                   DESIRED   CURRENT   READY     AGE
replicaset.apps/excited-elk-prometheus-alertmanager-68f4f57c97         1         1         0         3m
replicaset.apps/excited-elk-prometheus-kube-state-metrics-858d44dfdc   1         1         1         3m
replicaset.apps/excited-elk-prometheus-pushgateway-58bfd54d6d          1         1         1         3m
replicaset.apps/excited-elk-prometheus-server-5958586794               1         1         0         3m
[node1 ~]$
```



