# Deploy ASP.NET Core Website to Azure VM | IIS

## Prerequisites

Before performing this project, ensure you have:

- Basic knowledge of ASP.NET Core
- Access to an Azure VM
- IIS (Internet Information Services) installed on the Azure VM
- .NET Core SDK installed on your development machine

## What is .NET?

.NET is a software development framework created by Microsoft that provides a comprehensive and consistent programming environment for building, deploying, and running applications. It includes libraries, tools, and languages designed to make development easier and more efficient.

## What is a Framework?

### Purpose

A software framework provides a basic structure and set of tools for developing applications, so you don’t have to write everything from scratch.

### Example

If you’re building a website, a web framework like React or Angular offers pre-built components and a set of rules for organizing your code, making the development process faster and more manageable.

### Summary

A framework is like a helpful toolkit with instructions that streamlines the process of building something, whether it’s a website, an application, or any other project.

## .NET Overview

### 1. Framework Overview

- **What It Is**: .NET is a platform for building a wide range of applications, including web, desktop, mobile, and cloud-based applications. It includes a set of libraries, tools, and languages designed to make software development easier and more efficient.

- **Components**:
  - **.NET Core**: The cross-platform, open-source version of .NET that allows you to build applications that run on Windows, Linux, and macOS.
  - **.NET Framework**: The original version of .NET that runs primarily on Windows.
  - **Xamarin**: A set of tools for building mobile apps for iOS and Android using .NET.
  - **ASP.NET**: A framework for building web applications and services.

### 2. Why Use .NET?

- **Ease of Use**: .NET provides a lot of built-in functionality, which helps developers build applications faster.
- **Cross-Platform**: With .NET Core and .NET 5/6+, you can build applications that run on various operating systems.
- **Integration with Microsoft Products**: It integrates well with other Microsoft products and services, like Azure cloud services and SQL Server databases.

### 3. What Happens Without .NET?

Without .NET, you might need to:

- Install a web server.
- Write and configure server-specific scripts.
- Handle routing and server-side logic manually.

## Setting Up a Simple Web Server

### Without .NET

#### 1. Install a Web Server

- **Why It's Needed**: A web server listens for requests from users and responds with the appropriate information. Without a web server, your computer wouldn't be able to deliver web pages or other resources to users on the internet.
  
- **How to Do It**: Install a web server like Apache, Nginx, or use built-in ones provided by programming frameworks like Node.js or Python. Installation usually involves downloading the software and setting it up on your computer or server.

#### 2. Write and Configure Server-Specific Scripts

- **Why It's Needed**: You need to tell the web server how to handle requests. Scripts or files define what happens when someone visits your website.

- **How to Do It**: Write scripts using a programming language (like PHP, Python, or JavaScript) and configure files that tell the web server where to find these scripts and how to handle different types of requests.

#### 3. Handle Routing and Server-Side Logic Manually

- **Why It's Needed**: Routing directs requests to the right place, and server-side logic determines what the server does with data.

- **How to Do It**: Define routes and server-side logic in your scripts. Write code that decides if a request should show a webpage, perform a calculation, or fetch data from a database.

### With .NET

- **What You Do**:
  - Create a new project with `dotnet new webapp`.
  - Write your application code using ASP.NET Core.
  - Run the application locally with `dotnet run`, which starts the Kestrel web server for you.

## Benefits of Using .NET Core with IIS

Even when using .NET Core with IIS (Internet Information Services), some manual configuration is still required for IIS. However, .NET Core provides several key benefits and simplifications:

### 1. Simplified Development Process

- **Project Templates**: Use `dotnet new webapp` to quickly scaffold a new web application with default settings and structure.
- **Unified Framework**: ASP.NET Core integrates seamlessly with .NET Core libraries and tools, avoiding the need for multiple technologies.

### 2. Built-in Web Server

- **Kestrel**: ASP.NET Core applications run on Kestrel, a cross-platform web server included with .NET Core. This is useful for development and testing.
- **Benefit**: Kestrel is lightweight and fast, and it handles HTTP requests while you develop locally before deploying to IIS.

### 3. Configuration Management

#### What is Configuration Management?

Configuration management involves keeping track of how a machine or system is set up and ensuring it stays that way. It’s like maintaining a detailed list of how you like your kitchen organized, so it’s set up just how you like it.

#### What is Configuration Management in .NET Core?

Configuration management in .NET Core involves managing the settings and secrets your application needs to run, such as database connection strings, API keys, and other important settings.

##### Key Concepts

- **Flexible Configuration System**: .NET Core provides a system to handle configuration settings flexibly, adapting to different environments without hard-coding settings into your application code.
- **Configuration Sources**:
  - **appsettings.json**: A JSON file for storing default settings common across different environments.
  - **Environment Variables**: System environment variables that can override settings in `appsettings.json` and are used for sensitive information or varying settings between environments.
- **Environment-Based Configuration**: Different configurations for different environments (e.g., development, staging, production) allow tailoring settings without changing the code.

##### How You Benefit

- **Easier Management of Settings**: Store settings in configuration files or environment variables, making it easier to update settings without changing the code.
- **Different Configurations for Different Environments**: Use different configuration files or environment variables for development, staging, and production settings.
- **Safer Handling of Secrets**: Keep sensitive information out of your source code, preventing accidental exposure of secrets.

### 4. Cross-Platform Development

Develop and test on Linux or macOS, even if deploying on IIS.
