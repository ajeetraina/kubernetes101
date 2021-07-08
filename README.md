# Kubernetes For You

Are you new to Kubernetes? Want to build your career in Kubernetes?

Then Welcome ! You are at the right place.

This repository brings you tutorials that help you get hands-on experience using Kubernetes. Here you will find a mix of labs and tutorials that will help you, no matter if you are a beginner, SysAdmin, IT Pro or Developer. Yes, you read it correct ! Its $0 learning platform. You don't need any infrastructure. Most of the tutorials runs on Play with K8s Platform. This is a free browser based learning platform for you. Kubernetes tools like kubeadm, kompose & kubectl are already installed for you. All you need is to get started.

We recommend you start with one of our Beginners Guides, and then move to intermediate and expert level tutorials that cover most of the features of Kubernetes. For a comprehensive approach to understanding Docker, I have categorized it as shown below:

[Kubernetes for Beginners](https://github.com/ajeetraina/docker101/blob/master/play-with-kubernetes/beginners/README.md)<br>

[Kubernetes for Intermediate](https://github.com/ajeetraina/docker101/blob/master/play-with-kubernetes/intermediate/README.md)<br>

[Kubernetes for Advanced Users](https://github.com/ajeetraina/docker101/play-with-kubernetes/advanced/README.md)<br>

## Getting Started with Kubernetes

To get started with Kubernetes, follow the below steps:

-  Open https://labs.play-with-k8s.com/ on your browser


Click on Add Instances to setup first k8s node cluster

## Cloning the Repository

```
git clone https://github.com/ajeetraina/kubernetes101/
cd kubernetes101/install

```

## Bootstrapping the First Node Cluster

```
sh bootstrap.sh
```

## Adding New K8s Cluster Node

Click on Add Instances to setup first k8s node cluster

Wait for 1 minute time till it gets completed.

Copy the command starting with ```kubeadm join ....```. We will need it to be run on the worker node.


## Setting up Worker Node

Click on "Add New Instance" and paste the last kubeadm command on this fresh new worker node.

```
[node2 ~]$ kubeadm join --token 4f924f.14eb7618a20d2ece 192.168.0.8:6443 --discovery-token-ca-cert-hash  sha256:a5c25aa4573e06a0c11b11df23c8f85c95bae36cbb07d5e7879d9341a3ec67b3```
```

You will see the below output:

```
[kubeadm] WARNING: kubeadm is in beta, please do not use it for production clusters.
[preflight] Skipping pre-flight checks[discovery] Trying to connect to API Server "192.168.0.8:6443"
[discovery] Created cluster-info discovery client, requesting info from "https://192.168.0.8:6443"
[discovery] Requesting info from "https://192.168.0.8:6443" again to validate TLS against the pinned public key
[discovery] Cluster info signature and contents are valid and TLS certificate validates against pinned roots, will use API Server "192.168.0.8:6443"[discovery] Successfully established connection with API Server "192.168.0.8:6443"
[bootstrap] Detected server version: v1.8.15
[bootstrap] The server supports the Certificates API (certificates.k8s.io/v1beta1)
Node join complete:
* Certificate signing request sent to master and response
  received.
* Kubelet informed of new secure connection details.

Run 'kubectl get nodes' on the master to see this machine join.
[node2 ~]$
```

# Verifying Kubernetes Cluster

Run the below command on master node

```
[node1 ~]$ kubectl get nodes
NAME      STATUS    ROLES     AGE       VERSION
node1     Ready     master    15m       v1.11.3
node2     Ready     <none>    1m        v1.11.3
[node1 ~]$
```

## Adding Worker Nodes

```
[node1 ~]$ kubectl get nodes
NAME      STATUS     ROLES     AGE       VERSION
node1     Ready      master    18m       v1.11.3
node2     Ready      <none>    4m        v1.11.3
node3     Ready      <none>    39s       v1.11.3
node4     NotReady   <none>    22s       v1.11.3
node5     NotReady   <none>    4s        v1.11.3
[node1 ~]$
```

```
[node1 ]$ kubectl get po
No resources found.
```

```
[node1 ]$ kubectl get svc
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   1h
[node1 istio]$
```

# Kubernetes-Ready Solution

[ Demonstrating WordPress under Multi-Node K8s Cluster](https://github.com/ajeetraina/docker101/blob/master/play-with-kubernetes/intermediate/README.md)<br>
[ Deploying Nginx on Single Node K8s Cluster](https://github.com/ajeetraina/docker101/blob/master/play-with-kubernetes/beginner/nginx/README.md)<br>
[ Building Multi-Node Hadoop Cluster under K8s Cluster](https://github.com/ajeetraina/docker101/blob/master/play-with-kubernetes/intermediate/README.md)<br>








# Learn Kubernetes in 10 Days

[Day-0: What is Kubernetes? What are its components](https://github.com/ajeetraina/kubernetes101/blob/master/architecture/README.md)<br>
[Day-1: Getting Started with Pods, Services & Replicasets](https://github.com/ajeetraina/kubernetes101/blob/master/concept/day-1/getting-started.adoc)<br>
[Day-2: Kubernetes on AWS](https://github.com/ajeetraina/kubernetes-aws-workshop)<br>
[Day-3: Kubernetes on GCP](https://github.com/ajeetraina/kubernetes101/blob/master/labs/kubernetes-gce-lab/README.md)<br>
[Day-4: Kubernetes on Azure](https://github.com/ajeetraina/hands-on-with-kubernetes-azure)<br>
[Day-5: Kubernetes on Vagrant](https://github.com/ajeetraina/vagrant-kubernetes-lab)<br>
[Day-6: Kubernetes & Networking](https://collabnix.github.io/kubelabs/ClusterNetworking101/#Cluster-Networking)<br>
[Day-7: Kubernetes & Network Policy](https://collabnix.github.io/kubelabs/Network_Policies101/)<br>
[Day-8: Kubernetes on Monitoring](https://collabnix.github.io/kubelabs/Monitoring101/#Monitoring-in-Kubernetes)<br>
[Day-9: Kubernetes & Service Catalog](https://collabnix.github.io/kubelabs/ServiceCatalog101/what-is-service-catalog.html)<br>
[Day-10: Kubernetes & RBAC](https://collabnix.github.io/kubelabs/RBAC101/#role-based-access-control-rbac)<br>
[Day-11: Kubernetes & Ingress](https://collabnix.github.io/kubelabs/Ingress101/)<br>
[Day-12: Kubernetes and Jobs](https://collabnix.github.io/kubelabs/Jobs101/#creating-your-first-kubernetes-job)<br>

# Kubernetes on Collabnix.com

[5 Minutes to Bootstrap Kubernetes Cluster on GKE using Docker for Mac 18.03.0](http://collabnix.com/bootstrapping-kubernetes-cluster-using-docker-for-mac-18-03-0-ce-edition/)<br>
[Context Switching Made Easy under Kubernetes powered Docker for Mac 18.02.0](http://collabnix.com/namespace-context-toggling-made-easy-under-docker-for-mac-18-02-release/)<br>
[2-minutes to Kubernetes Cluster on Docker for Mac 18.01 using Swarm CLI](http://collabnix.com/running-kubernetes-cluster-on-docker-for-mac-18-01-using-swarm-cli/)<br>
[3 Minutes to Single Node Kubernetes cluster on Docker for Mac Platform](http://collabnix.com/3-minutes-to-single-node-kubernetes-cluster-on-docker-for-mac-platform/)<br>
[When Kubernetes Meet Docker Swarm for the First time under Docker for Mac 17.12 Release](http://collabnix.com/integration-of-docker-swarm-kubernetes-under-docker-for-mac-platform/) <br>
[A First Look at Kubernetes Integrated Docker For Mac Platform](http://collabnix.com/a-first-look-at-kubernetes-integrated-docker-for-mac-platform/)<br>
[When Moby Meet Kubernetes for the first time](http://collabnix.com/when-linuxkit-meet-kubernetes-for-the-first-time/)<br>
[How to Build Kubernetes Cluster using CRI-containerd & Moby](http://collabnix.com/building-multi-node-kubernetes-cluster-using-linuxkit-cri-containerd/) <br>
[Getting Started with Multi-Node Kubernetes Cluster using LinuxKit](http://collabnix.com/getting-started-with-multi-node-kubernetes-cluster-using-linuxkit/)

# Kubernetes & OpenFaas

[Deploying OpenFaas on K8s]()<br>

# Kubernetes Stuffs

[Abstract - Kubernetes]()<br>



