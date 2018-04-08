# Set up a local VM cluster

* Deploy a Kubernetes cluster using Vagrant

The Kubernetes project has a Vagrant 'cloud-provider' with ready-made scripts
to set-up and provision a VM-based (Virtualbox) cluster. There are separate
VMs for the master and node(s). See [Getting started with Vagrant](https://github.com/kubernetes/kubernetes/blob/release-1.0/docs/getting-started-guides/vagrant.md) for more
detailed information.

## Set up

Use a custom-built release package - 
[download here]() and extract the archive.

```
export KUBERNETES_PROVIDER=vagrant
./cluster/kube-up.sh
```

This will now provision a single master VM (kubernetes-master) and a node VM (kubernetes-minion-1).
By default, each VM in the cluster is running Fedora.

## Verify the cluster is up

```
./cluster/kubectl.sh get nodes
```
