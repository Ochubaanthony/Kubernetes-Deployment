# Kubernetes-Deployment
Steps to deploy Kubernetes using minikube
Steps
Nano deployment.yaml

Paste this 

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
	ports:
	- containerPort: 80

Steps
kubectl apply -f deployment.yaml
kubectl get deploy
kubectl get pods
kubectl get rs


Steps
Open Another Terminal
kubectl get pods -w

YOU NOTICE IT DELETED AND RECREATE A NEW POD Immediately


ON THE OLD TERMINAL
kubectl delete pod nginx-deployment-647677fc66-wwvgq
kubectl get pods



Steps 

OLD TERMINAL
Go Back to deployment.yaml
Increase the replicas pod to 3
nano deployment.yaml
kubectl apply -f deployment.yaml

kubectl get pods
kubectl delete pods nginx-deployment-647677fc66-cbz9p



NEW TERMINAL
kubectl get pods -w                       ( you will see 3 pods)
kubectl get pods -w 













Here’s a concise summary of the explanation:

Kubernetes Deployment is a higher-level abstraction over Pods used to manage containerized applications more efficiently. While Containers are created using platforms like Docker (via CLI commands), Kubernetes runs them within Pods, which define the configuration in a YAML file. A Pod can host one or more containers that share network and storage, which is useful for tightly coupled applications (e.g., with a sidecar container).

However, Pods alone lack advanced features like:
	•	Auto-healing (restarting containers if they fail)
	•	Auto-scaling (adjusting the number of containers based on load)

To enable these, Kubernetes uses Deployments, which:
	•	Define desired state (e.g., number of replicas) in a YAML file.
	•	Create an intermediate ReplicaSet, a controller that ensures the specified number of Pods are always running.
	•	Support zero-downtime deployments, high availability, and easier updates.

Summary of Differences:
	•	Container: Runs your app, usually via Docker.
	•	Pod: Kubernetes unit that wraps one or more containers.
	•	Deployment: Manages Pods using ReplicaSets for scaling, healing, and updates.

Here’s a summarized explanation of how Kubernetes Deployments work and the role of ReplicaSets and Controllers:

Summary:
	•	A Deployment in Kubernetes manages application updates and scaling by creating a ReplicaSet.
	•	The ReplicaSet is a Kubernetes Controller—a special component responsible for maintaining the desired state defined in the Deployment YAML manifest (e.g., number of pods).
	•	The Controller ensures that what you specify (the desired state) matches what actually exists in the cluster (the actual state).
	•	If a pod crashes or is deleted, the ReplicaSet automatically creates a new pod to match the desired number—this is called auto-healing.
	•	Kubernetes has default controllers (like ReplicaSet, Deployment, etc.) and allows for custom controllers (e.g., Argo CD, Admission Controllers).
	•	Interview Questions:
	1.	Difference between Container, Pod, and Deployment
	2.	Difference between Deployment and ReplicaSet
	•	Deployment creates and manages the ReplicaSet.
	•	ReplicaSet is what actually maintains the pod count (auto-healing).
	•	To practice, use kubectl commands with a running Kubernetes cluster (e.g., via Minikube or AWS). You can view current pods with kubectl get pods and delete resources with kubectl delete.
