![JFrog MCP Server](https://avatars.githubusercontent.com/u/499942?s=200&v=4) 

# JFrog MCP Server

A Model Context Protocol (MCP) server that brings the power of the JFrog platform directly to your development environment through AI-powered interactions.

## Overview

The Model Context Protocol (MCP) enables AI systems to connect with external tools, data, and services using a standardized, lightweight interface. The **JFrog MCP Server** extends this capability by integrating JFrog platform functionality into IDEs and AI coding assistants like GitHub Copilot and Cursor.

With JFrog MCP Server, you can interact with your JFrog platform using natural language queries, getting real-time, actionable information without leaving your development environment.

## Key Capabilities

Transform your development workflow with these AI-powered JFrog integrations:

### 🏗️ Resource Management
- Create and manage JFrog projects and repositories
- View and configure platform components
- Access organizational resources through natural language queries

### 🔍 Artifact Search & Discovery  
- Execute powerful AQL (Artifact Query Language) searches
- Find artifacts across your organization's repositories
- Discover dependencies and their relationships

### 📦 Package Catalog & Curation
- Access comprehensive package information and version history
- Check vulnerability status and security ratings
- Verify package curation and approval status
- Review license requirements and compliance

### 🛡️ Security & Compliance Monitoring
- Generate real-time DevSecOps security reports
- Monitor critical CVEs and vulnerability severity levels
- Assess vulnerability applicability to your specific environment
- Track security posture across your artifact ecosystem

## Real-World Use Cases

Leverage JFrog MCP Server for these common development scenarios:

### 🚀 **Secure Development Workflow**
*"Show me all packages in my project with high-severity vulnerabilities"*
- Quickly identify security risks during development
- Get instant remediation recommendations
- Ensure compliance with security policies

### ✅ **Package Approval & Governance**  
*"Is the latest version of React approved for use in our organization?"*
- Verify package curation status before adding dependencies
- Check organizational approval policies
- Access license compliance information

### 📊 **Project & Artifact Management**
*"Create a new repository for my microservice and show me the deployment artifacts from last week"*
- Streamline project setup and configuration
- Track artifact lifecycle and deployment history
- Manage repository permissions and settings

### 🔄 **Dependency Analysis**
*"Find all projects using vulnerable versions of log4j and show me the upgrade path"*
- Identify affected projects across your organization
- Plan coordinated security updates
- Track dependency relationships and impact

## Remote Server Architecture

The JFrog MCP Server operates as a cloud-hosted service with several key advantages:

- **🔄 Always Up-to-Date**: Automatically receive new features and improvements without manual updates
- **🔐 Secure Authentication**: OAuth-based connection eliminates API key management  
- **☁️ Zero Installation**: No local setup or maintenance required
- **⚡ High Performance**: Cloud-optimized for fast response times

You connect to the JFrog MCP Server using OAuth authentication, providing secure access to your JFrog platform while maintaining enterprise security standards.

## Getting Started

### Prerequisites
- JFrog Cloud (SaaS) subscription
- Admin access to enable the MCP Server
- Compatible MCP client (VS Code, Cursor, or other MCP-enabled IDE)

### Setup Process

**Step 1: Enable JFrog MCP Server**  
An Admin user must [enable the JFrog MCP Server](https://jfrog.com/help/r/jfrog-integrations-documentation/enable-the-jfrog-mcp-server) on your JFrog Platform Deployment (JPD).

**Step 2: Configure Your MCP Client**  
[Add the JFrog MCP Server to your MCP client](https://jfrog.com/help/r/jfrog-integrations-documentation/add-the-jfrog-mcp-server-to-an-mcp-client) using the configuration examples below.

**Step 3: Save Configuration**  
Save the configuration file in your MCP client's settings.

**Step 4: Authenticate**  
Restart or refresh your MCP client. An OAuth window will open in your browser to authorize the connection.

**Step 5: Start Using**  
Once authenticated, you can begin interacting with your JFrog platform through natural language queries in your IDE.

### Configuration Examples

#### Visual Studio Code
```json
{
  "mcp": {
    "servers": {
      "jfrog": {
        "url": "https://<JFROG_PLATFORM_URL>/mcp"
      }
    }
  }
}
```

#### Cursor
```json
{
  "mcpServers": {
    "jfrog": {
      "url": "https://<JFROG_PLATFORM_URL>/mcp"
    }
  }
}
```

> **Note**: Replace `<JFROG_PLATFORM_URL>` with your actual JFrog platform URL (e.g., `mycompany.jfrog.io`)

## Next Steps

Once configured, try these example queries in your AI assistant:
- *"Show me the security status of packages in my current project"*
- *"Create a new Maven repository called 'my-app-releases'"*
- *"Find all Docker images tagged with 'latest' in the last 30 days"*
- *"What are the license requirements for the packages I'm using?"*

For more detailed information and advanced usage, visit the [JFrog MCP Server documentation](https://jfrog.com/help/r/jfrog-integrations-documentation).
