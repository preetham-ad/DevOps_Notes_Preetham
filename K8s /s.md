#KUBERNETES PODS | Deploying first app

# In k8s why cant you deploy your containers directly, why do you need to use pods?

In docker when you want to deploy a container you simply perform 'docker run args'. In k8s you pass those user defined commands and specifications to pod.yml file. Instead of command line, you are trying to put everything in YAML file.

# A pod can have single or group of containers.

There are some advantages when you put group of containers in a pod like shared network, shared storage.

You access the app using the cluster ip address that k8s gave for the pod (i.e. kubeproxy).

# To interact with k8s, you use kubectl.
# give me steps to setup minikube, kubectl , and commands to create pods and check the app

#Pod YAML File
1. Definition
Basic Resource: Defines a single Pod which may contain one or more containers.
Static: Describes how a specific Pod should be configured, but does not include mechanisms for managing updates or scaling.

Features
No Built-in Scaling: A Pod definition does not include scaling or rolling update features.
No Self-Healing: If a Pod fails, Kubernetes does not automatically recreate it.
Single Instance: Manages only a single instance of the container

#Deployment YAML File
A Deployment is a higher-level abstraction that manages a set of Pods. It provides mechanisms for scaling, rolling updates, and self-healing. Here’s what a deployment.yaml file does:
Features:
Scaling: Automatically adjusts the number of Pod instances based on the replicas field.
Rolling Updates: Updates applications with zero downtime by gradually replacing old Pods with new ones.
Self-Healing: Recreates failed Pods to maintain the desired replica count.
Declarative Management: Ensures the desired state is achieved through a declarative configuration.
