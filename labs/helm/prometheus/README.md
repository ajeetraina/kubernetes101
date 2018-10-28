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


```
[node1 ~]$ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈ Happy Helming!⎈
```


```
$helm install stable/prometheus
``

This will throw error.
```
namespaces "default" is forbidden: User "system:serviceaccount:kube-system:default" cannot get namespaces in the namespace "default"
```

How to fix?

```
kubectl create serviceaccount --namespace kube-system tiller
```
```
  serviceaccount "tiller" created
```

```
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
```

```
clusterrolebinding "tiller-cluster-rule" created
```

```
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}' 
```

```
deployment "tiller-deploy" patched
```

```
[node1 ~]$ helm list
NAME            REVISION        UPDATED                         STATUS          CHART                   APP VERSION     NAMESPACE
excited-elk     1               Sun Oct 28 10:00:02 2018        DEPLOYED        prometheus-7.3.4        2.4.3           default
```





