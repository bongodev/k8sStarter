# Minikube Installation Guide for Ubuntu

This guide provides step-by-step instructions for installing Minikube on Ubuntu. You can run a single-node Kubernetes cluster locally or in AWS for development and testing purposes.

## Pre-requisites

* Ubuntu OS
* sudo privileges
* Virtualization support enabled (Check with `egrep -c '(vmx|svm)' /proc/cpuinfo`, 0=disabled 1=enabled) 

---

## Step 1: Update System Packages

Update your UBUNTU package lists to make sure you are getting the latest version and dependencies.

```bash
sudo apt update
```


## Step 2: Install Required Packages

Install some basic required packages.

```bash
sudo apt install -y curl wget apt-transport-https
```

---

## Step 3: Install Docker

Minikube can run a Kubernetes cluster either in a VM or locally via Docker. This guide demonstrates the Docker method.

```bash
sudo apt install -y docker.io
```


Start and enable Docker.

```bash
sudo systemctl enable --now docker
```

Add current user to docker group (To use docker without root)

```bash
sudo usermod -aG docker $USER
```
Now, logout from the machine and connect again.

Alternatively (without sudo reboot):
```bash
sudo chown $USER /var/run/docker.sock
```

---

## Step 4: Install Minikube

First, download the Minikube binary using `curl`:

```bash
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64  #download
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64 #install Minikube
```

Make it executable and move it into your path:

```bash
chmod +x minikube
sudo mv minikube /usr/local/bin/
```

Check minikube version
```bash
minikube version
```

---

## Step 5: Install kubectl

Download kubectl, which is a Kubernetes command-line tool.

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
Make it executable and move it into your path:

```bash
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

---

## Step 6: Start Minikube

Now, start Minikube with the following command:

```bash
minikube start --driver=docker --vm=true 
```

If you already have Docker installed, start Minikube with the following command:

```bash
minikube start 
```

This will start a single-node Kubernetes cluster inside a Docker container and your Kubernetes cluster should be ready.

---

## Step 7: Check Cluster Status

Check the cluster status with:

```bash
minikube status
```



You can also use `kubectl` to interact with your cluster:

```bash
kubectl get nodes
```

---

## Step 8: Stop Minikube

When you are done, you can stop the Minikube cluster with:

```bash
minikube stop
```

---

## Optional: Delete Minikube Cluster

If you wish to delete the Minikube cluster entirely, you can do so with:

```bash
minikube delete
```

---

Cheers!
