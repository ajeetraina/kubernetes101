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
$helm inspect stable/prometheus

##
  name: server

  ## Prometheus server container image
  ##
  image:
 ...
 
 ```
 
 ```
 [node1 ~]$ helm reset --force
Tiller (the Helm server-side component) has been uninstalled from your Kubernetes Cluster.
```

## Creating RBAC config file

```
[node1 ~]$ helm init --service-account tiller --upgrade -i registry.cn-hangzhou.aliyuncs.com/google_containers/tiller:v2.7.0 --stable-repo-url https://kubernetes.oss-cn-hangzhou.aliyuncs.com/charts
$HELM_HOME has been configured at /root/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.

Please note: by default, Tiller is deployed with an insecure 'allow unauthenticated users' policy.
To prevent this, run `helm init` with the --tiller-tls-verify flag.
For more information on securing your installation see: https://docs.helm.sh/using_helm/#securing-your-helm-installation
Happy Helming!
```
