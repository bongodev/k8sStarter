# deploy-sample-application

Follow the instructions after the Minikube cluster configurations are completed. We will deploy and make rolling update (i.e. app version).

## Create a Namespace

In Kubernetes namespaces provide a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace. Run the below command

    kubectl create namespace sample-app

## Create a Kubernetes deployment

A Kubernetes Deployment tells Kubernetes how to create or modify instances of the pods that hold a containerized (docker our case) application. Deployments can help to efficiently scale the number of replica pods, enable the rollout of updated code in a controlled manner, or roll back to an earlier deployment version if necessary.

Apply the deployment manifest to your cluster.

    kubectl apply -f 01-create-deployment.yaml

Review the deployment configurations.

    kubectl describe deployments.apps --namespace sample-app sample-deployment


## Create a service

A service allows you to access all replicas through a single IP address or name.

There are different types of Service objects, and the one we want to use for testing is called ClusterIP or LoadBalancer, which means an external load balancer for Minikube.

Apply the service manifest to your cluster.

	kubectl apply -f 02-service-to-expose-deployment.yaml

View all resources that exist in the sample-app namespace.

	kubectl get all --namespace sample-app


## Deploy a new application version (rolling out)

In kubernetes you can easily deploy a new version of an existing deployment by updating the image details.

Apply `03-update-or-rollout-deployment.yaml` deployment manifest to your cluster.

    kubectl apply -f 03-update-or-rollout-deployment.yaml

Kubernetes performs a rolling update by default to minimize the downtime during upgrades and create a replica set and pods.
Review the deployment configurations and verify the image details

    kubectl describe deployments.apps --namespace sample-app   sample-deployment

## Check if nginx is working from terminal (not on the browser):
	minikube ip #it will return the minikube IP

	curl http://<ip got from minikube ip command>:30080  # i.e. http://192.168.49.5:30080

	You should see html content
## Once you're finished with the sample application, you can remove the sample namespace, service, and deployment with the following command.

    kubectl delete namespace sample-app
