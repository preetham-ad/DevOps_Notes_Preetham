# IIS Installation

## Prerequisites

### Operating System

**Why**: IIS needs to be installed on a supported version of Windows Server. Each version has specific features and capabilities, so it's important to use a compatible version.

**What it Does**: Ensures that the environment meets the requirements for IIS to function correctly.

### Administrative Access

**Why**: Installing and configuring IIS requires making changes to system settings and files that only an administrator can perform.

**What it Does**: Grants you the necessary permissions to install and configure server roles.

### Updates

**Why**: Ensures that you have the latest security patches and bug fixes, which can affect the stability and security of IIS.

**What it Does**: Keeps the server environment current and secure.

## Installation Steps

1. **Open Server Manager**

   **Why**: Server Manager is the tool used to manage server roles and features.

   **What it Does**: Provides access to the interface where you can add and manage server roles.

2. **Add Roles and Features**

   **Why You Need to Add Roles and Features**:

   - **Enable Functionality**: Roles and features are like building blocks for what your server can do. For example, to set up IIS (Internet Information Services) for hosting websites, you need to add the Web Server (IIS) role. This role enables your server to serve web pages.

   - **Customize Server Capabilities**: Allows you to tailor the server's functionality to meet your specific needs. For instance, if you need support for web applications, you might also add features like ASP.NET. If you need file transfer capabilities, you might add the FTP Server feature.

3. **Role-based or Feature-based Installation**

   **Why**: This tells the wizard you want to install something new, not just manage existing stuff.

   **What it Does**: Focuses on installing new roles or features rather than just managing them.

4. **Select Destination Server**

   **Why**: You need to pick which server you want to install IIS on if you have multiple servers.

   **What it Does**: Chooses the specific server where IIS will be installed.

5. **Select Server Roles**

   **Why**: Here, you choose what specific role you want to install—in this case, IIS for web hosting.

   **What it Does**: Sets IIS as the role to be installed and adds any additional features needed for it.

6. **Select Features**

   **Why**: Lets you choose extra tools or features that IIS might need, like support for .NET applications.

   **What it Does**: Adds additional functionality based on your needs.

7. **Web Server Role (IIS)**

   **Why**: This gives you a summary of what IIS does and what will be installed.

   **What it Does**: Confirms that IIS is the role you’re installing and explains what it includes.

8. **Select Role Services**

   **Why**: Lets you pick specific services that IIS should have, like FTP or extra management tools.

   **What it Does**: Customizes IIS by selecting additional services or tools you might need.

---

In summary, these steps guide you through selecting and installing IIS on your server, along with any extra features or services you might need.
