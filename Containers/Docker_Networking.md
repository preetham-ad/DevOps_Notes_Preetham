# Docker Networking Explained

Docker provides several networking options to manage how containers communicate with each other and with the outside world. These options help you control visibility, security, and network configuration.

## Key Networking Concepts

1. **Bridge Network**: 
   - This is the default network type. Docker creates a virtual network bridge (`docker0`) on the host. Containers connected to this bridge can communicate with each other and the host. By default, they are isolated from external networks unless port forwarding is configured.

2. **Custom Bridge Network**:
   - You can create custom bridge networks to control how containers communicate. Containers on the same custom bridge network can talk to each other, but containers on different networks cannot communicate unless explicitly configured.

3. **Host Network**:
   - Containers share the host’s network stack and IP address, providing high performance but less isolation.

4. **Overlay Network**:
   - Used for multi-host networking, often in Docker Swarm or Kubernetes, allowing containers on different hosts to communicate as if they were on the same network.

5. **None Network**:
   - No networking. The container is isolated from all networks.

## Scenario 1: Isolation of Containers

In this scenario, you have two containers running on the same host:

- **Container1 (C1)**: Running `app1` (login app)
- **Container2 (C2)**: Running `app2` (payment app)

By default, Docker connects these containers to the `docker0` bridge network, which allows them to communicate with each other and the host. However, this default setup might not meet your security requirements because:

- **Security Risk**: Both containers can potentially talk to each other and the host, which might expose sensitive data or services.

**Solution**: Create a **Custom Bridge Network** to enhance security.

### Steps to Create and Use a Custom Bridge Network:

1. **Create a Custom Bridge Network**:
   ```bash
   docker network create --driver bridge my_custom_network
2. **Run Containers on the Custom Network**:
For Container1:
```bash
Copy code
docker run -d --name container1 --network my_custom_network app1_image
```
For Container2:
```bash
Copy code
docker run -d --name container2 --network my_custom_network app2_image
```
**Why This Works**:
Isolation: Containers on a custom bridge network can communicate with each other but not with containers on the default docker0 network or other networks. This improves security and reduces the risk of unauthorized access.

## Scenario 2: Communication Between Containers
In this scenario, you need app1 on Container1 to communicate with app2 on Container2.

### Steps to Enable Communication:
**Use the Same Custom Bridge Network**:
Ensure both containers are connected to the same custom bridge network, as shown above.

**Service Discovery**:
Containers on the same custom bridge network can communicate using container names as hostnames. For example, Container1 can access Container2 using the hostname container2.

In Container1 (running app1), you can access Container2 (running app2) using:
```curl http://container2:port```

## Why This Works:

**Network Configuration**: By placing both containers on the same custom bridge network, Docker manages the network routing and DNS resolution for you.
**Service Discovery**: Docker provides automatic DNS resolution for container names within the same network, allowing containers to find each other using their names.
Summary
**Default Network (docker0)**: Allows all containers on the same host to communicate with each other and the host. This may not be secure if you need isolation.
**Custom Bridge Network**: Provides better security and isolation while still allowing containers to communicate with each other if they are on the same network.
**Container Communication**: Within the same custom network, containers can use names to communicate with each other, simplifying service discovery and interactions.
In summary, Docker networking allows you to control how containers communicate, both with each other and with external systems. Using custom networks, you can enforce isolation and security while enabling necessary communication between containers.
