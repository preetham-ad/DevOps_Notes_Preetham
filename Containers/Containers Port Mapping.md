# Accessing Your Containerized Django App on EC2

## Issue: Unable to Access the App

After running your containerized Django app on an EC2 instance, you’re facing an issue where you cannot access the application from the EC2 instance’s IP address. The error indicates that port mapping is required.

## Why Port Mapping is Needed

Port Mapping connects the ports of your Docker container to the ports on the EC2 instance. Without proper port mapping, the EC2 instance cannot communicate with the Docker container’s internal ports. Therefore, even though your Django app is running inside the container, it isn’t exposed to the outside world (including your browser) without port mapping.

## Steps to Resolve the Issue

### 1. Verify Docker Container Setup

Make sure your Docker container is running and listening on the correct internal port (e.g., port 8000 for Django).

```bash
docker ps
```
This command shows the list of running containers. Ensure that your Django container is listed.

## 2. Update Docker Run Command with Port Mapping
When running your Docker container, you need to map the internal port (where Django is running) to an external port on your EC2 instance. For example:

```bash
docker run -d -p 80:8000 my-django-app
```
- d: Runs the container in detached mode (background).
- p 80:8000: Maps port 80 on the EC2 instance to port 8000 inside the Docker container.
This means that requests to port 80 of your EC2 instance will be forwarded to port 8000 of your container.

## 3. Check EC2 Security Group Settings
Ensure that the EC2 instance’s security group allows incoming traffic on the port you’re mapping. For example, if you mapped port 80 on the EC2 instance:

Go to the EC2 Dashboard.
Find and select your EC2 instance.
Click on the Security tab.
Edit the inbound rules of the security group to allow HTTP traffic on port 80.

### Port 80 Overview

Port 80 is the default port used by the Hypertext Transfer Protocol (HTTP) for web traffic. Below is an explanation of its purpose and usage.

### **Protocol**

- **HTTP**: Port 80 is used for HTTP connections, which are responsible for transferring web pages and related content over the internet.

### **Usage**

- **Web Traffic**: Port 80 is commonly used to serve web pages. When you enter a URL into your web browser without specifying a port number, it defaults to port 80 for HTTP traffic.

### **Purpose**

- **Web Servers**: Port 80 allows web servers to communicate with web browsers and other clients to deliver content such as HTML pages, images, and other resources.

### **Example**

- **Web Server Configuration**: A web server (e.g., Apache, Nginx) configured to listen on port 80 will handle incoming HTTP requests on that port.
- **Accessing Websites**: Visiting a website by entering `http://example.com` in a browser will connect to the web server at `example.com` on port 80 by default.



## 4. Access the Application
After running the Docker container with port mapping and adjusting security group settings:

Open a web browser.
Navigate to http://<EC2_PUBLIC_IP>.
This should display your Django application if everything is set up correctly.

## Summary
- Port Mapping: Ensure you’re using the correct Docker run command with port mapping (-p 80:8000).
- Security Groups: Verify that your EC2 instance’s security group permits traffic on the mapped port (e.g., port 80).
- Container Check: Confirm that the Docker container is running and accessible.

