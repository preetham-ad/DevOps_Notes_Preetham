# Kubernetes Pods | Deploying Your First App

## Why Use Pods in Kubernetes?

In Kubernetes (K8s), containers are not deployed directly. Instead, they are managed within Pods. Here's why Pods are used:

### Direct Container Deployment

In Docker, you deploy containers using `docker run` with various arguments.

**Example:**
```bash
docker run -d --name myapp myapp-image
```
# Kubernetes Pods

In K8s, you define containers through a Pod YAML file. Pods can contain one or multiple containers.

## Advantages of Pods

- **Shared Network:** Containers within a Pod share the same network namespace, including IP address and ports.
- **Shared Storage:** Containers can share storage volumes.

## Accessing the Application

Access is done using the Cluster IP provided by K8s, managed by kube-proxy.
# Interacting with Kubernetes

To manage Kubernetes, use `kubectl`. Here are the key commands and steps:

## 1. Set Up Minikube and kubectl

### Start Minikube

```bash
minikube start
```
### Verify Minikube Status

```bash
minikube status
```
## 2. Create and Manage pods

```bash
kubectl apply -f pod.yaml
```
### Get Pod Details
```bash
kubectl get pods -o wide
```
### View Pod logs
```bash
kubectl logs <pod-name>
```
## 3. Access the Application

### Expose the Pod (Create a Service):

```bash
kubectl expose pod <pod-name> --port=80 --target-port=80 --name=<service-name>
```
### Get Service URL:
```bash
minikube service <service-name>
```
### Pod YAML File

#### Definition
- **Basic Resource**: Defines a single Pod, which may contain one or more containers.
- **Static**: Describes the Pod configuration without mechanisms for managing updates or scaling.

#### Features
- **No Built-In Scaling**: A Pod definition does not support scaling or rolling updates.
- **No Self-Healing**: Kubernetes does not automatically recreate Pods if they fail.
- **Single Instance**: Manages only a single instance of a container or a group of containers.

---

### Deployment YAML File

#### Definition
- A Deployment is a higher-level abstraction that manages a set of Pods. It includes mechanisms for scaling, rolling updates, and self-healing.

#### Features
- **Scaling**: Automatically adjusts the number of Pod instances based on the replicas field.
- **Rolling Updates**: Updates applications with zero downtime by gradually replacing old Pods with new ones.
- **Self-Healing**: Recreates failed Pods to maintain the desired replica count.
- **Declarative Management**: Ensures the desired state is achieved through a declarative configuration.


