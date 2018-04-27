# Deploying OpenFaas on Docker for Mac 18.05.0 RC1

## Pre-requisite:

- Docker for Mac 18.05.0 RC1
-Enable Kubernetes

## Cloning the Fass-netes Repository

```
git clone https://github.com/openfaas/faas-netes
```

```
git clone https://github.com/openfaas/faas-netes
Cloning into 'faas-netes'...
remote: Counting objects: 3517, done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 3517 (delta 7), reused 12 (delta 3), pack-reused 3494
Receiving objects: 100% (3517/3517), 4.21
```

## Bring up OpenFaas-netes Stack

```
kubectl apply -f ./namespaces.yml,./yaml
```

```
namespace "openfaas" created
namespace "openfaas-fn" created
deployment "alertmanager" created
service "alertmanager" created
configmap "alertmanager-config" created
deployment "faas-netesd" created
service "faas-netesd" created
deployment "gateway" created
service "gateway" created
deployment "nats" created
service "nats" created
deployment "prometheus" created
service "prometheus" created
configmap "prometheus-config" created
deployment "queue-worker" created
serviceaccount "faas-controller" created
role "faas-controller" created
rolebinding "faas-controller-fn" created
```


```
kubectl get po --namespace openfaas
NAME                            READY     STATUS    RESTARTS   AGE
alertmanager-864794d49d-zvqs7   1/1       Running   0          3m
faas-netesd-5d58bd4c7c-575l2    1/1       Running   0          3m
gateway-649bbbf944-9z2zf        1/1       Running   1          3m
nats-6c4f7df-9q9sf              1/1       Running   0          3m
prometheus-d67b9ff9c-v44jz      1/1       Running   0          3m
queue-worker-5dfb769469-2lh8f   1/1       Running   0          3m
```


