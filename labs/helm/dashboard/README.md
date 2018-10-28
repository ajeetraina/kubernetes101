

```
[node1 ~]$ helm install stable/kubernetes-dashboard
NAME:   loopy-anteater
LAST DEPLOYED: Sun Oct 28 10:06:29 2018
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Service
NAME                                 AGE
loopy-anteater-kubernetes-dashboard  0s

==> v1beta1/Deployment
loopy-anteater-kubernetes-dashboard  0s

==> v1/Pod(related)

NAME                                                 READY  STATUS             RESTARTS  AGE
loopy-anteater-kubernetes-dashboard-d49cf484b-s87mm  0/1    ContainerCreating  0         0s

==> v1/Secret

NAME                                 AGE
loopy-anteater-kubernetes-dashboard  0s

==> v1/ServiceAccount
loopy-anteater-kubernetes-dashboard  0s

==> v1beta1/Role
loopy-anteater-kubernetes-dashboard  0s

==> v1beta1/RoleBinding
loopy-anteater-kubernetes-dashboard  0s


NOTES:
*********************************************************************************
*** PLEASE BE PATIENT: kubernetes-dashboard may take a few minutes to install ***
*********************************************************************************

Get the Kubernetes Dashboard URL by running:
  export POD_NAME=$(kubectl get pods -n default -l "app=kubernetes-dashboard,release=loopy-anteater" -o jsonpath="{.items[0].metadata.name}")
  echo https://127.0.0.1:8443/
  kubectl -n default port-forward $POD_NAME 8443:8443

[node1 ~]$
```
