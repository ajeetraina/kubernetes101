# What is Kubernetes?

Kubernetes (commonly referred to as K8s) is an orchestration engine for container technologies such as Docker and rkt that is taking over the DevOps scene in the last couple of years. It is already available on Azure and Google Cloud as a managed service.

Kubernetes can speed up the development process by making easy, automated deployments, updates (rolling-update) and by managing our apps and services with almost zero downtime. It also provides self-healing. Kubernetes can detect and restart services when a process crashes inside the container. Kubernetes is originally developed by Google, it is open-sourced since its launch and managed by a large community of contributors.

Any developer can package up applications and deploy them on Kubernetes with basic Docker knowledge.

# What is K8s made up of?

## Kubectl:

- A CLI tool for Kubernetes

![alt text](https://github.com/ajeetraina/kubernetes101/blob/master/architecture/kubernetes-kubectl.png)



## Master Node:

![alt text](https://github.com/ajeetraina/kubernetes101/blob/master/architecture/kubernetes-kubelet.png)

- The main machine that controls the nodes
- Main entrypoint for all administrative tasks
- It handles the orchestration of the worker nodes

## Worker Node

![alt text](https://github.com/ajeetraina/kubernetes101/blob/master/architecture/kubernetes-worker-node.png)

- It is a worker machine in Kubernetes (used to be known as minion)
- This machine performs the requested tasks. Each Node is controlled by the Master Node
- Runs containers inside pods
- This is where the Docker engine runs and takes care of downloading images and starting containers

## Kubelet

[alt text](https://github.com/ajeetraina/kubernetes101/blob/master/architecture/kubernetes-kubelet.png)

- Primary node agent
- Ensures that containers are running and healthy

