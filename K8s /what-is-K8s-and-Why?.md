# Kubernetes (K8s)

## What is Kubernetes (K8s)?

Kubernetes, often abbreviated as K8s, is an open-source platform designed for automating the deployment, scaling, and management of containerized applications. It helps manage containerized applications across a cluster of machines, providing features like self-healing, auto-scaling, and load balancing.

## Why K8s?

### Problem 1: Single Host Limitations

- **Containers are Ephemeral:** Containers are short-lived. Let's say you have only one host with Docker installed and you create 100 containers. If container 1 uses too many resources like memory, container 100 might not start at all or may die immediately. So, one container can impact another container.

### Problem 2: Auto-Healing is Missing in Docker

- **Manual Monitoring Required:** If a container goes down or gets killed, the app running inside it becomes inaccessible. You would need to manually check and restart the container. If you have 10,000 containers in your organization, as a DevOps engineer, you can't keep performing `docker ps` and manually check which containers are running.

### Problem 3: Auto-Scaling

- **Scaling Challenges:** Docker does not provide built-in support for auto-scaling, making it difficult to automatically adjust resources based on demand.

### Problem 4: Enterprise-Level Features Missing

- **Enterprise App Needs:** An enterprise app is a software application designed to meet the needs of a large organization or business rather than individual users. Docker is a minimalistic platform that lacks enterprise-level support. It doesn't provide enterprise standards like load balancers, firewalls, auto-scaling, auto-healing, or API gateways.

## How K8s Solves These Problems

### Solution to Problem 1: Cluster Architecture

- **Cluster Management:** K8s uses a cluster architecture, which solves the problem of a single host by maintaining a group of nodes (master and worker nodes). For example, if you have K8s with two nodes and container 1 on node 1 is affecting container 99, K8s will immediately move container 99 to node 2. If a faulty app (pod) on a node is affecting other apps (pods) on the same node, K8s will move the problematic pod to a different node.

### Solution to Problem 2: Auto-Scaling with Replication Controllers

- **Replication Sets and Controllers:** K8s solves this problem with replication sets and replication controllers. You can manually auto-scale the containers using YAML files, such as `replication-set.yaml` or `deployment.yaml`, where you can specify that you want to scale from 1 container to 10. You can also use the Horizontal Pod Autoscaler (HPA) feature for automatic scaling.

### Solution to Problem 3: Auto-Healing

- **Auto-Healing Feature:** K8s provides auto-healing capabilities. It uses the API server to monitor when a container goes down and automatically rolls out a new container to replace it.

### Solution to Problem 4: Enterprise-Level Support

- **Enterprise Features:** Docker is not used in production environments on its own. You can use Docker Swarm, but not Docker alone, because it does not provide enterprise-level support. K8s is a tool that originated from Google. Google used a specific tool called Borg, and K8s is considered a part of Borg. Google has built an enterprise-level container orchestration platform with K8s.

## Does K8s Solve These Problems 100%?

- **Not Perfect:** In a nutshell, no. K8s does not solve these problems 100% perfectly. However, the Cloud Native Computing Foundation (CNCF) is working to make K8s a better solution.
