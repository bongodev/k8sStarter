# KIND Cluster Setup Guide

  Kind requires at least:

    - 2 CPUs

    - 4 GB memory

    - 10 GB disk space

## 1. Installing Docker, KIND and kubectl
Install KIND and kubectl using the provided [script](https://github.com/bongodev/k8sStarter/blob/main/kind/installer.sh):
```bash
  chmod 777 installer.sh
  ./installer.sh
```

This will Docker KIND and kubectl!


## 2. Setting Up the KIND Cluster
Create a cluster:

  kind create cluster --config=kind-config.yml --name=bongodev-cluster

Verify the cluster:
```bash
  kubectl get nodes
  kubectl cluster-info --context kind-bongodev-cluster
```
## 3. Accessing the Cluster
Use kubectl to interact with the cluster:

  kubectl cluster-info



## 4. Setting Up the Kubernetes Dashboard
Deploy the Dashboard
Apply the Kubernetes Dashboard manifest:

  kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml

Create an Admin User


  kubectl apply -f dashboard-admin-user.yml

Get the Access Token
Retrieve the token for the admin-user:


  kubectl -n kubernetes-dashboard create token admin-user

Copy the token for use in the Dashboard login.

Access the Dashboard
Start the Dashboard using kubectl proxy:

```bash

kubectl proxy
```
Open the Dashboard in your browser:

```bash

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```
Use the token from the previous step to log in.

## 5. Deleting the Cluster
Delete the KIND cluster:
```bash

kind delete cluster --name bongodev-cluster
```

## 6. Notes

Multiple Clusters: KIND supports multiple clusters. Use unique --name for each cluster.
Custom Node Images: Specify Kubernetes versions by updating the image in the configuration file.
Ephemeral Clusters: KIND clusters are temporary and will be lost if Docker is restarted.

