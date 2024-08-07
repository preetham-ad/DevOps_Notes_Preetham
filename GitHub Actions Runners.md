# GitHub Actions Runners Explained

## What Are GitHub Actions Runners?

**GitHub Actions Runners** are the agents(Virtual Machines) that execute the tasks defined in your GitHub Actions workflows. They perform actions like running tests, building code, or deploying applications based on the instructions provided in your workflow files.

## Types of GitHub Actions Runners

### 1. GitHub-Hosted Runners

**GitHub-Hosted Runners** are provided and managed by GitHub. 

- **Features:**
  - **Preconfigured:** Comes with many common tools and software pre-installed.
  - **Automatic Updates:** Regularly updated by GitHub.
  - **Scalability:** Automatically scales based on the number of workflows.

- **Use Case:** Ideal for most standard workflows where you don’t need special configurations or tools.

### 2. Self-Hosted Runners

**Self-Hosted Runners** are machines that you set up and manage yourself.

- **Features:**
  - **Customizable:** You can install specific software or tools needed for your workflows.
  - **Controlled Environment:** You control the environment and configuration.
  - **Cost:** You are responsible for the infrastructure costs.

- **Use Case:** Useful for custom setups, special hardware requirements, or specific network configurations.

## Why Configure Security Group (SG) Rules for Self-Hosted Runners?

When using self-hosted runners, configuring Security Group (SG) rules is essential to ensure proper functionality.

### Inbound and Outbound Rules

#### Inbound Rules

**Inbound Rules** control the traffic that is allowed to reach your self-hosted runner from the outside world.

- **Why Needed:** To ensure the runner can receive job requests from GitHub.
- **Configuration:**
  - **Allow HTTP (port 80) and HTTPS (port 443) traffic** from GitHub’s servers.
  - **Source:** `0.0.0.0/0` to allow traffic from anywhere or specify GitHub IP ranges.

#### Outbound Rules

**Outbound Rules** control the traffic that your self-hosted runner can send out to the outside world.

- **Why Needed:** To ensure the runner can send job results and access necessary external resources.
- **Configuration:**
  - **Allow HTTP (port 80) and HTTPS (port 443) traffic** to communicate with GitHub and other services.
  - **Destination:** `0.0.0.0/0` to allow traffic to any external resource or specify specific IP ranges.

## Configurations Required on AWS EC2 or Cloud-Hosted Virtual Machine

###  Install and Configure the Self-Hosted Runner

1. **Download and Install the Runner:**
   - Follow GitHub’s [official documentation](https://docs.github.com/en/actions/hosting-your-own-runners) for downloading and setting up the runner.

2. **Register the Runner:**
   - Register the runner with your GitHub repository using the provided token.

3. **Start the Runner:**
   - Run the installation script to start the runner service.

## Summary

- **GitHub Actions Runners:** Execute tasks from your workflow files. You can use GitHub-hosted runners or set up self-hosted runners.
- **Security Groups:** Required for configuring inbound and outbound traffic to ensure proper communication with GitHub and other external resources.
- **AWS Configuration:** Set up inbound and outbound rules to allow HTTP/HTTPS traffic, and follow GitHub’s guide to install and configure self-hosted runners.

Feel free to adjust the configurations according to your specific requirements and cloud provider’s capabilities.
