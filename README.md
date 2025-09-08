# JFrog Remote MCP Server  
The Model Context Protocol (MCP) connects AI systems with external tools, data, and services using a standardized, lightweight interface.  

**JFrog MCP Server** integrates JFrog configuration and usage information in IDEs and coding assistants such as Copilot or Cursor. This improves and enriches the response to AI queries.   
JFrog MCP Server acts as a bridge between natural language requests and Frog APIs and documentation resources. This initial Beta release provides a core set of tools that let you use AI to optimize the following tasks:
* Create and view projects, repositories, and other JFrog components.  
* Poll JFrog for detailed information on package status, including vulnerability status of open-source packages.  
* Review the components currently in use in your organization.

Additional tools and capabilities will be added to the JFrog MCP Server on an ongoing basis.  

**Remote Server Implementation:** The JFrog MCP Server is maintained on the JFrog Cloud, and the tools it provides to the client are constantly updated - you automatically get new features and improvements as they are released.   
You connect to the JFrog MCP server using OAuth for authentication. This eliminates the need to manage API keys, and no installation or upgrade is required after you enable the implementation.  

## Setting up JFrog MCP Server  
The JFrog MCP Server is available to JFrog users with a Cloud (SaaS) subscription.  
An Admin user must [enable the JFrog MCP Server](https://jfrog.com/help/r/jfrog-integrations-documentation/enable-the-jfrog-mcp-server)  on a JPD in the subscription.  
You can then [add the JFrog MCP Server to an MCP](https://jfrog.com/help/r/jfrog-integrations-documentation/add-the-jfrog-mcp-server-to-an-mcp-client)


1. Log in to an IDE or AI tool that functions as the MCP client.     
2. Use the JFrog MCP Server URL to as the Server to the MCP client.

The following example shows MCP Server definition in Visual Studio Code:  
```json 
  "mcp": {  
        "servers": {  
            "jfrog": {  
                "url":"https://<​**​JFROG_PLATFORM_URL​**​>/mcp"  
            }  
        }  
```  
The following example shows MCP Server definition in Cursor:  
```json  
{  
  "mcpServers": {  
    "jfrog": {  
      "url":"https://<​**​JFROG_PLATFORM_URL​**​>/mcp"  
    }  
  }  
}  
```  

3. Save the configuration file.  
4. Restart or refresh your MCP client. An OAuth window opens in your browser. 
5. Follow the prompts to authorize your MCP client to access the JFrog MCP Server.

# Features  
## Supported Tools  
The JFrog MCP Server provides the following actions, which are exposed as "tools" to MCP Clients. You can use these tools to interact with your JFrog projects using natural language commands.  

![MCP Client](https://avatars.githubusercontent.com/u/499942?s=200&v=4) 
