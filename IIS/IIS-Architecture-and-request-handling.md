# IIS Architecture and Request Handling

## Overview

IIS (Internet Information Services) architecture is divided into two main modes: **Kernel mode** and **User mode**.

- **Kernel Mode**: This is the part of IIS that is built into Windows and comes with the operating system. It operates at a low level with complete control over the hardware and memory.
- **User Mode**: This mode contains the services and processes that can be managed by the user, such as through Task Manager. It operates at a higher level with limited access, making it safer and more controlled.

## Kernel Mode Components

### HTTP.sys

- **HTTP.sys** is a kernel-mode driver and acts as an HTTP listener, responsible for monitoring and handling incoming HTTP requests.
- **Function**: It intercepts HTTP requests before they reach the user mode and efficiently manages web traffic.

## User Mode Components

### WAS (Windows Activation Service) and WWW (World Wide Web Publishing Service)

- Both WAS and WWW services run in the same `SVCHOST.exe` process and are crucial for managing IIS configuration and operations.

#### Windows Activation Service (WAS)
- **Role**: WAS is responsible for managing application pools and worker processes (`w3wp.exe`). It handles the execution and processing of web applications.
- **Configuration**: WAS reads the `applicationHost.config` file, which contains all the settings related to websites, bindings, and application pools.

#### World Wide Web Publishing Service (WWW Service)
- **Role**: The WWW Service reads configuration data from the `applicationHost.config` file and communicates with `HTTP.sys` to instruct it on which IPs and ports (bindings) to listen to.
- **Function**: It configures `HTTP.sys` to handle requests correctly based on the settings specified in the configuration file.

## Additional Content

In the Kernel mode, we have `Http.sys` driver (HTTP listener) which is responsible for monitoring and listening for the HTTP traffic.

In the user mode, we have the following services: **WAS** and **WWW**. Both services run in the same `SVCHOST.exe` process. Mainly, WAS and WWW are responsible for reading the `ApplicationHosts.config` file. This file contains the configuration such as bindings, your websites, your data, your application pools, and so on.

So, the WWW service will tell the HTTP listener in the kernel's group using the HTTP APIs to listen on the IPs and ports found in that configuration file. These IPs and ports are simply the bindings that you configured on your server. So simply, the WWW service is responsible for contacting the HTTP listener to tell it about the bindings.

While the WAS service will actually handle the management of application pools, and also the code, the processing operation, and the execution of the applications. The worker process (`w3wp.exe`) is inside the application pool, so the WAS service will also handle the management of that process.

## IIS Request Handling Process

### 1. Client Browser Makes an HTTP Request
- **Process**: When a user enters a URL in the browser or clicks a link, the browser sends an HTTP request to the web server to fetch a resource (e.g., a webpage or file).

### 2. HTTP.sys Intercepts the Request
- **Process**: The HTTP request first reaches `HTTP.sys`, which intercepts it and begins processing.

### 3. HTTP.sys Contacts WAS
- **Process**: `HTTP.sys` contacts the Windows Activation Service (WAS) to determine how to handle the request. It requests configuration details based on the server’s settings.

### 4. WAS Requests Configuration from `applicationHost.config`
- **Process**: WAS reads the `applicationHost.config` file, which contains settings for all the websites, their configurations, and the application pools.

### 5. WWW Service Receives Configuration Information
- **Process**: The WWW Service receives the necessary configuration from WAS, including details about the application pool and the website configuration.

### 6. WWW Service Configures `HTTP.sys`
- **Process**: The WWW Service configures `HTTP.sys` using the retrieved configuration information, ensuring it can correctly handle the request.

### 7. WAS Starts a Worker Process (`w3wp.exe`)
- **Process**: WAS starts (or reuses) a worker process (`w3wp.exe`) from the appropriate application pool. This process is where the actual web application code runs.

### 8. Worker Process Handles the Request
- **Process**: The worker process processes the request by running the necessary web application code, fetching data, and rendering the webpage or resource.

### 9. `HTTP.sys` Sends the Response Back to the Client
- **Process**: After the worker process generates the response, `HTTP.sys` sends it back to the client’s browser, completing the request-response cycle.

## Summary

- The client sends an HTTP request.
- `HTTP.sys` intercepts the request and communicates with WAS.
- WAS fetches the necessary configuration, and the WWW Service configures `HTTP.sys`.
- A worker process (`w3wp.exe`) processes the request and returns a response.
- The response is sent back to the client.

This is a high-level overview of how IIS handles incoming web requests, from the moment a client makes a request to when the response is delivered.

