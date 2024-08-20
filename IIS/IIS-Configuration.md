# Configuration of IIS

## Steps

### 1. Open IIS Manager

**Why**: IIS Manager is the tool used for managing IIS configurations and settings.

**What it Does**: Launches the interface where you can configure IIS settings and manage sites.

### 2. Configure Default Website

**Why**: The Default Web Site is the initial site created with IIS. Configuring it helps you understand the basic setup.

**What it Does**: Allows you to view and modify the settings for the default site.

### 3. Bindings

**Why**: Bindings configure how IIS handles requests for different URLs or ports.

**What it Does**: Sets up how the server will respond to requests for specific IP addresses, hostnames, or ports.

#### Scenario

You have a server with IIS hosting two websites:

- **Website A** at `exampleA.com`
- **Website B** at `exampleB.com`

Both websites use the same IP address (`192.168.1.10`) and port (`80`).

#### How It Works

When a request arrives:

- **For `http://exampleA.com`**: IIS checks the bindings, finds a match for `exampleA.com`, and serves Website A.
- **For `http://exampleB.com`**: IIS checks the bindings, finds a match for `exampleB.com`, and serves Website B.

Bindings ensure the correct website is delivered based on the URL requested.

### 4. Set Up Websites

**Why**: To host multiple websites, you need to create and configure each site.

**What it Does**: Adds new websites to IIS with specific settings for their location and access.

### 5. Configure Application Pools

**Why**: Application pools isolate different web applications for security and performance reasons.

**What it Does**: Sets up pools to manage how applications run and resource allocation.

#### Scenario

Imagine you have a server with IIS that hosts two different web applications:

1. **App A**: A high-traffic e-commerce site.
2. **App B**: A small internal company blog.

#### Why Configure Application Pools?

**Isolation for Security and Performance**: By placing these apps in separate application pools, you ensure that:

- **Security**: If App A has a security issue, it won't affect App B.
- **Performance**: Resource usage by App A won't impact App B, and vice versa.

#### How It Works

a. **Create Application Pools**:
   - **App Pool A**: Dedicated to handling requests for App A.
   - **App Pool B**: Dedicated to handling requests for App B.

b. **Assign Applications to Pools**:
   - Assign App A to **App Pool A**.
   - Assign App B to **App Pool B**.

c. **Configure Pool Settings**:
   - Set specific resource limits and recycling schedules for each pool based on the needs of each app.

When a request comes in:

- **For App A**: IIS processes it through **App Pool A**, ensuring it gets the appropriate resources and operates independently of other apps.
- **For App B**: IIS processes it through **App Pool B**, maintaining isolation and performance specific to this app.

**Application pools** help manage how different web applications run, improving security and optimizing resource use by keeping them separate.

### 6. Configure Security

**Why**: Security settings control who can access your websites and how they can interact with them.

**What it Does**: Configures authentication and authorization rules to protect your sites.

### 7. Test Your Setup

**Why**: Ensures that the IIS installation and configuration are correct and that the websites are accessible.

**What it Does**: Verifies that everything is set up properly by accessing the sites through a web browser.

---

This guide outlines the steps to configure IIS, including how to manage sites, bindings, application pools, security, and testing your setup.
