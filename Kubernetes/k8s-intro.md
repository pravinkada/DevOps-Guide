# Kubernetes:

https://www.linkedin.com/posts/abhipraydhoble_kubernetes-k8s-cloudcomputing-activity-7217124292373696515-iwUc?utm_source=share&utm_medium=member_desktop

**What is Kubernetes?**
Kubernetes is an open-source platform used to automate the deployment, scaling, and management of containerized applications. It is like a traffic controller for containerized applications. It ensures that these applications are running efficiently and reliably, by managing their deployment, scaling, and updating processes. 

Kubernetes Architecture:
![kubernetes-cluster-architecture](https://github.com/abhipraydhoble/devops-B-34/assets/122669982/5eddf6eb-2bd3-4e57-9f3b-90e7567fca84)


A Kubernetes cluster consists of control plane nodes and worker nodes.
**Control Plane:** The control plane is responsible for container orchestration and maintaining the desired state of the cluster. It has the following components.

- kube-apiserver
- etcd
- kube-scheduler
- kube-controller-manager
- cloud-controller-manager
  
**1.kube-apiserver:**
- The kube-api server is the central hub of the Kubernetes cluster that exposes the Kubernetes API End users,
- and other cluster components, talk to the cluster via the API server.
- Kubernetes api-server is responsible for the following
- ***API management:*** Exposes the cluster API endpoint and handles all API requests.
    Authentication (Using client certificates, bearer tokens, and HTTP Basic Authentication)
    and Authorization (ABAC and RBAC evaluation)It is the only component that communicates with etcd.
- api-server coordinates all the processes between the control plane and worker node components.
  
**2.Etcd:**
- It is a brain of the Kubernetes cluster, it acts as a database and stores data in key-value format.
- etcd stores all configurations, states, and metadata of Kubernetes objects (pods, secrets, daemonsets, deployments, configmaps, statefulsets, etc).
  
**3.kube-scheduler:**
- The kube-scheduler is responsible for scheduling Kubernetes pods on worker nodes.
  
**4.Kube Controller Manager :** 
- Controllers are programs that runs continuously and watches the actual and desired state of objects.
- If there is a difference in the actual and desired state,
- it ensures that the kubernetes resource/object is in the desired state.
  
**Worker Node:**
The Worker nodes are responsible for running containerized applications. The worker Node has the following components.
- kubelet
- kube-proxy
- Container runtime

**1. Kubelet**
Kubelet is an agent component that runs on every node in the cluster. it does not run as a container instead runs as a daemon, managed by systemd.

**2. Kube proxy**
Kube proxy deals with networking, When you create the service object, 
it gets a virtual IP assigned to it. It is called clusterIP. 
It is only accessible within the Kubernetes cluster.

**3. Container Runtime**:
container runtime is a software component that is required to run containers. 
Container runtime runs on all the nodes in the Kubernetes cluster. 
It is responsible for pulling images from container registries,
running containers, allocating and isolating resources for containers, 
and managing the entire lifecycle of a container on a host

**5.Pod :**
Pod is the smallest deployable unit . A Pod encapsulates one or more containers, storage resources, 
a unique network IP, and options that govern how the container’s should run. 
Containers within a Pod share the same network namespace and can communicate with each other using localhost.

## Minikube Installation on AWS EC2

## Step 1: Create an AWS EC2 instance with Ubuntu 22
Instance Size: t2.large with 2 CPUs, 32 GB Storage

## Step 2 : Install Docker
````
sudo apt update
````
Next, install a few prerequisite packages which let apt use packages over HTTPS:
````
sudo apt install apt-transport-https ca-certificates curl software-properties-common
````
Then add the GPG key for the official Docker repository to your system:
````
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
````
Add the Docker repository to APT sources:
````
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
````
Update your existing list of packages again for the addition to be recognized:
````
sudo apt update
````
Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:
````
apt-cache policy docker-ce
````
Finally, install Docker:
````
sudo apt install docker-ce
````
````
sudo systemctl status docker
````
Executing the Docker Command Without Sudo
````
sudo usermod -aG docker ubuntu
````
````
newgrp docker
````
## Install kubectl
Download the latest release with the command:
````
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
````
Validate the binary 
````
 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
````
Validate the kubectl binary against the checksum file:
````
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
````
Install kubectl:
````
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
````
Note:
If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:
````
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
````
````
kubectl version --client
````
## Step 4: Install Minikube
````
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
````
````
sudo install minikube-linux-amd64 /usr/local/bin/minikube
````
````
minikube start
````
````
minikube stop
````

