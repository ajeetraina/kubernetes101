# Setting up Kubernetes on Google Cloud Engine

# Build the Kubernetes Cluster

In this section, you will find code blocks with commands  for you to copy & paste into the Google Cloud Shell (remote terminal window). We have excluded the command prompt itself (the dollar sign `$`) from the snippets. 

**Tips for those who have not used a command line in ages**

It may take few minutes for a command prompt to respond. However, if it ever gets stuck you can use `Ctrl+C` to interrupt the current command and get back to the command prompt. 

You can use the `Up Arrow` to navigate to previous commands in the command history. 

To copy from the terminal window, simply highlight the desired text and it will be auto-copied. You can then use paste it as usual.

## 1. Sign In To Google Cloud

Navigate to the Google Cloud portal: https://console.cloud.google.com/ 

For this workshop we will use the web-based terminal window, Google Cloud Shell, to avoid differences between operating systems and personal configurations. 

Open the Google Cloud Shell

![Cloud Shell](https://image.ibb.co/ccoxLF/cloudshell.png)

List all the projects on Google Cloud to make sure everything is working and you're in the right place.

```
gcloud projects list
```

If you used Google Cloud before you may have more than one project. Make sure you change to your preferred project. If you never used Google Cloud before you can skip this command.

```
gcloud config set project [PROJECT_ID]
```

Set default zone in Google Cloud for the workshop

```
gcloud config set compute/zone us-east1-c
```

## 2. Clone the Workshop Git Repository

Clone the following GitHub repo into the Cloud Shell to get local access to the workshop demo files

```
git clone https://github.com/ajeetraina/hands-on-with-kubernetes-gke 
```

If you type `ls` into the command line you should see a new `hands-on-with-kubernetes-gke` directory. 

Change into the workshop directory you just cloned

```
cd hands-on-with-kubernetes-gke
```

## 3. Provision a Cluster

Run the following command to create a 3-node Kubernetes cluster in Google Container Engine (GKE). This may take a minute to respond and will run for several minutes while the cluster is provisioned.

```
gcloud container clusters create "k8sworkshop" \
  --zone "us-east1-c" \
  --machine-type "n1-standard-1" \
  --image-type "GCI" --disk-size "100" \
  --scopes cloud-platform \
  --num-nodes "3"
``` 

When the command is finishing executing, you will see output like this
![Imgur](http://i.imgur.com/zAMyyez.png)

You can navigate to the Container Engine section of the Google Cloud Portal https://console.cloud.google.com/kubernetes/list. You should see your newly created Kubernetes cluster listed there.

You can also navigate to the Compute Engine section to see the three virtual machines that were provisioned to power the new Kubernetes cluster https://console.cloud.google.com/compute/instances  

## 4. Connect To The Cluster

Make sure the Kubernetes command-line client (`kubectl`) is up to date

```
gcloud components install kubectl
```

Configure `kubectl` with the workshop cluster context/credentials 

```
gcloud container clusters get-credentials k8sworkshop
```

Now verify that `kubectl` can connect to the cluster

```
kubectl cluster-info
```

Since we are in the Cloud Shell (essentially a VM in Google Cloud) we need to modify the Kubernetes Dashboard UI Service to expose it to the Internet

```
kubectl get svc kubernetes-dashboard -n kube-system -o yaml | \
sed "s/ClusterIP/LoadBalancer/" | \
kubectl apply -f - -n kube-system
```

Get the IP address of the Dashboard

```
kubectl get svc kubernetes-dashboard -n kube-system
```

The `EXTERNAL-IP` column may show `<pending>` for a short while while the Google Load Balancer is configured. You can simply use the `Up Arrow` to show the previous command and run it again until you see an IP address has been allocated.

Grab the `EXTERNAL-IP` address (sample highlighted below) and paste it into a new browser tab or window (your IP will be different from one shown below) 

![IP Address](http://i.imgur.com/i1hlPV2.png)

## 5. Run "Hello World"

Deploy a "Hello, World!" application to get something up and running on your new cluster

```
kubectl run hello-world \
--replicas=5 --labels="run=load-balancer-example" \
--image=gcr.io/google-samples/node-hello:1.0  \
--port=8080
```

Navigate to the "Workloads" section in the Kubernetes Dashboard you previously opened and you should see the new Deployment, ReplicaSet and Pods being created

![Imgur](http://i.imgur.com/j8oVACv.png)

## 6. Tour of Dashboard (the official UI of Kubernetes)

Instructor will give a tour of the Kubernetes Dashboard and cover the constructs of Kubernetes. 

They will then cover the demo apps found here https://github.com/apprenda/hands-on-with-kubernetes-gke/tree/master/docs/demos
