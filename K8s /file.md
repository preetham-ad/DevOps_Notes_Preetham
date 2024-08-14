DevOps Notes

#API GATEWAY Imagine you have a website that interacts with several
services like user management, payment processing, and product catalog.
Instead of each service handling requests directly, an API Gateway sits
in front and manages all requests, directing them to the right service
and handling tasks like authentication and logging.

In essence, an API Gateway helps streamline communication between your
application and its users or other services, making the system more
efficient and manageable.

\# Microservices architecture Benefits Observed Famous companies like
Amazon, Airbnb, Netflix have seen various benefits from adopting
microservices architecture, including:

Scalability: Ability to scale individual services independently based on
demand. Flexibility: Easier to deploy new features and updates without
affecting the entire system. Resilience: Improved fault isolation,
reducing the impact of failures on the overall system. Speed: Faster
development cycles and deployment times due to independent service
management.

#Why Use Docker Driver with Minikube? Minikube on Docker might seem like
using containers to orchestrate containers, but here's why it's a
practical and effective approach:

Efficiency and Speed:

Faster Start-Up: Docker containers start quickly as they share the host
OS kernel, avoiding the overhead of full VMs. Resource Efficiency:
Containers are lightweight and use fewer resources, ideal for
development environments with limited resources. Local Development and
Testing:

Quick Setup: Minikube on Docker provides a local Kubernetes cluster
efficiently without the overhead of VMs, simplifying development and
testing. Consistency: Docker ensures a consistent environment that
closely matches production setups where Docker is commonly used.
Simplicity:

Single Host Setup: Running Kubernetes in Docker avoids the need for
managing separate VMs, streamlining the setup process. Integrated Tools:
Both Docker and Kubernetes are container-focused, making Docker a
natural choice for running Kubernetes locally.

\# How It Works Under the Hood When using the Docker driver with
Minikube:

Docker Container: Minikube sets up a Docker container on your host
machine. This container acts as the VM for the Kubernetes cluster.
Kubernetes Components: Inside this Docker container, Minikube installs
and configures Kubernetes components like the API server, scheduler, and
controller manager. Networking: Minikube configures networking so that
you can interact with the Kubernetes cluster running inside the Docker
container from your local machine
