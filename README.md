![MCP Client](https://avatars.githubusercontent.com/u/499942?s=200&v=4)

# JFrog Remote MCP Server

The Model Context Protocol (MCP) connects AI systems with external tools, data, and services using a standardized, lightweight interface.

**JFrog MCP Server empowers developers, bringing the advanced capabilities of the JFrog platform to the development environment.** The JFrog MCP Server integrates with IDEs and AI coding assistants such as VS Code, Cursor, Claude, Kiro, and Codex to respond to natural-language AI queries with rich, actionable information from the JFrog platform.

Among the capabilities you can access with direct, friendly AI interactions:

* **Resource Management**: Create and view projects, repositories, and other JFrog components.
* **Artifact & Build Discovery**: Find packages and their versions, locate where artifacts are stored, and search builds using AQL.
* **Catalog and Curation**: Access package information, versions, and vulnerabilities, and check curation status.
* **Security Monitoring**: Get Xray security summaries and policy violations for artifacts, check an artifact's scan/indexing status, and trace every resource impacted by a specific CVE or package.

**Use these resources and real-time information for various use cases. For example:**

* **Ensure that only approved packages are used by developers during coding.**
* **Query the JFrog Catalog about OSS package versions, changes in reported vulnerabilities, and license requirements.**
* **Track and manage JFrog Projects and artifacts.**

**And much more.** See the full [tool reference](TOOLS.md) for everything the server exposes.

> **Note:** The JFrog MCP Server is now **generally available (GA)** on JFrog Cloud (SaaS). The self-managed server is in Beta. Individual tools marked **Beta** in the [tool reference](TOOLS.md) are experimental and must be enabled for your environment.

## Remote Server Implementation

The JFrog MCP Server is hosted on JFrog Cloud, and the tools it provides to the client are continuously updated — you automatically get new features and improvements as they are released, with **no installation or upgrade required** on the client side.

You connect to the JFrog MCP Server using OAuth for authentication. This eliminates the need to manage API keys.

> **Note:** Because this is a remote server, the tool set evolves on the server. The [`TOOLS.md`](TOOLS.md) reference reflects the current tool surface.

## Set up the JFrog MCP Server

The JFrog Remote MCP Server is generally available (GA) to JFrog users with a Cloud (SaaS) subscription.

> **Subscription information:** Supported on the **Cloud (SaaS)** and **Self-Managed** platforms for all licenses.

> **Self-Managed (Beta):** A self-managed JFrog MCP Server is also available. See [MCP Server Installation](https://docs.jfrog.com/installation/docs/mcp) for Helm and Docker Compose deployment.

1. An Admin user must [enable the JFrog MCP Server](https://jfrog.com/help/r/jfrog-integrations-documentation/enable-the-jfrog-mcp-server) on a JPD in the subscription.
2. You can then [add the JFrog MCP Server to an MCP client](https://jfrog.com/help/r/jfrog-integrations-documentation/add-the-jfrog-mcp-server-to-an-mcp-client).
3. Save the configuration file.
4. Restart or refresh your MCP client. An OAuth window opens in your browser.
5. Follow the prompts to authorize your MCP client to access the JFrog MCP Server.

In the examples below, replace `<JFROG_PLATFORM_URL>` with your JFrog platform URL (for example, `https://mycompany.jfrog.io`).

### Visual Studio Code

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

### Cursor

```json
{
  "mcpServers": {
    "jfrog": {
      "url": "https://<JFROG_PLATFORM_URL>/mcp"
    }
  }
}
```

For more MCP clients (Kiro, Claude, Codex, and others), see [Add the JFrog MCP Server to an MCP client](https://docs.jfrog.com/integrations/docs/add-the-jfrog-mcp-server-to-an-mcp-client).

## Tools

The server exposes over 100 tools across Access, Artifactory, Security, Curation, Distribution, Grid, Workers, OneModel, Event, Evidence, and AppTrust.

See the full reference in [`TOOLS.md`](TOOLS.md).

## Documentation

* [JFrog MCP Server for SaaS](https://docs.jfrog.com/integrations/docs/jfrog-mcp-server)
* [Enable the JFrog MCP Server](https://jfrog.com/help/r/jfrog-integrations-documentation/enable-the-jfrog-mcp-server)
* [Add the JFrog MCP Server to an MCP client](https://docs.jfrog.com/integrations/docs/add-the-jfrog-mcp-server-to-an-mcp-client)
* [Self-Managed MCP Server Installation (Beta)](https://docs.jfrog.com/installation/docs/mcp)
