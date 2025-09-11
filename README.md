![MCP Client](https://avatars.githubusercontent.com/u/499942?s=200&v=4) 

# JFrog Remote MCP Server

The Model Context Protocol (MCP) connects AI systems with external tools, data, and services using a standardized, lightweight interface.  
**JFrog MCP Server empowers developers, bringing the advanced capabilities of the JFrog platform to the development environment.** JFrog  MCP Server integrates in IDEs and coding assistants such as Copilot or Cursor to respond to natural-language AI queries with rich, actionable information from the JFrog platform.

Among the capabilities you can access with direct, friendly AI interactions:

* Resource Management: Create and view projects, repositories, and other JFrog components.  
* Artifact Search: Execute powerful AQL queries to search for artifacts used within your organization.  
* Catalog and Curation: Access package information, versions, vulnerabilities, and check curation status  
* Security Monitoring: generate real-time DevSecOps reports on critical CVEs, severity and applicability of vulnerabilities.

**Use these resources and real-time information for various use cases. For example:**

* **Ensure that only approved packages are used by developers during coding**  
* **Query JFrog Catalog about OSS package versions, changes in reported vulnerabilities, and license requirements**  
* **Track and manage JFrog Projects and artifacts**

**And much more.**

**Remote Server Implementation**: The JFrog MCP Server is maintained on the JFrog Cloud, and the tools it provides to the client are constantly updated \- you automatically get new features and improvements as they are released.   
You connect to the JFrog MCP server using OAuth for authentication. This eliminates the need to manage API keys, and no installation or upgrade is required after you enable the implementation.

## Set up JFrog MCP Server

The JFrog MCP Server is available to JFrog users with a Cloud (SaaS) subscription.  
1\. An Admin user must [enable the JFrog MCP Server](https://jfrog.com/help/r/jfrog-integrations-documentation/enable-the-jfrog-mcp-server) on a JPD in the subscription.  
2\. You can then [add the JFrog MCP Server to an MCP client](https://jfrog.com/help/r/jfrog-integrations-documentation/add-the-jfrog-mcp-server-to-an-mcp-client)   
3\. Save the configuration file.  
4\. Restart or refresh your MCP client. An OAuth window opens in your browser.   
5\. Follow the prompts to authorize your MCP client to access the JFrog MCP Server.

The following example shows MCP Server definition in Visual Studio Code:  
```json  
{
    "mcp":  
        "servers": {  
            "jfrog":   
                "url":"https://<​​JFROG_PLATFORM_URL​​>/mcp" 
            } 
        }
```  
The following example shows MCP Server definition in Cursor:  
```json  
{  
  "mcpServers": {  
    "jfrog": {  
      "url":"https://<​​JFROG_PLATFORM_URL​​>/mcp"
    }  
  }  
}
```
