## Chat with Oracle Database in natural language with SQLcl MCP Server

![Apex](/docs/assets/MCP/mcp-1.png)

### Introduction:
The Oracle SQLcl **Model Context Protocol** (MCP) Server transforms how you interact with the Oracle Database by enabling seamless communication with Artificial Intelligence (AI) applications.
The SQLcl MCP server recieves its directives from the AI Agent, acting upon your requests and communicating with the database on your behalf. 
This new way of working with your Oracle database allows for a more natural/plain language, conversation-based interaction.

### Pre-Requisite:
**1. VS Code installed**

**2. Configured an Oracle database connecting using SQL Developer Extension for VS Code**, see my last blog post [Connect to Oracle Database with VS Code using SQL Developer Extension and SQLcl](https://mksingla.github.io/2025/11/27/Install-SQL-Developer-Extension-for-VS-Code-and-SQLcl.html)

**3. Configure your preferred client**, I am configuring **Cline in VS Code**. Once configured, the MCP client autonomously handles server startup, manages its life cycle, and ensures clean termination upon session completion, while enabling Oracle Database operations through natural conversations.

- Open VC Code and click **Extensions** on the sidebar, enter cline in search field and install it.
   
![Apex](/docs/assets/MCP/mcp-2.png)

 - Click the Select Model/API Provider text. Chose your API Provider, I am using free grok model here

![Apex](/docs/assets/MCP/mcp-3.png)

**4. Configure SQLcl MCP Server**

   Navigate to the VS Code Command Palette. In the search field enter the following text: **Configure Cline SQLcl MCP**

   ![Apex](/docs/assets/MCP/mcp-4.png)

   Press enter to priew the **cline_mcp_settings.json** configuration file. We dont need to change anything here, save the file.

   ![Apex](/docs/assets/MCP/mcp-5.png)

   Now you should see **sqlcl** listed under the Installed MCP server.

   ![Apex](/docs/assets/MCP/mcp-61.png)

   When you expend the SQLcl MCP server, you can see all the **6 tools** used by this server

   ![Apex](/docs/assets/MCP/mcp-62.png)
   
   

### Testing Steps:
   
   **1.** Click on Cline extension and ensure you see the Agent prompt, **Plan** and **Act** modes.

   ![Apex](/docs/assets/MCP/mcp-7.png)

   **2.** Enable **Plan** mode and in the input area of Cline, enter the following propmt and click enter. (test1 is my DB connection name)
      "connect to my database as the test1 and run a test query to make sure everything is working as expected"
      
   ![Apex](/docs/assets/MCP/mcp-71.png)

   **3.** Cline will create a plan and respond by asking permission to use your SQLcl MCP Server via the list-connections tool.
   
   ![Apex](/docs/assets/MCP/mcp-8.png)
   
   **4.** Select the Approve button to allow the Agent to continue its plan.
          The Agent will use your Oracle Database connection and execute a query and ask to toggle to **Act** to implement this plan.

   ![Apex](/docs/assets/MCP/mcp-9.png)

   **5.** Once Click on Act, it will again ask to approve before Cline will use the **connect** tool to connect a database.

   ![Apex](/docs/assets/MCP/mcp-10.png)

   **6.** Click **Approve** and now it connected to database. Now its asking approval to use **run-sql** tool to run the query on DB, Click on Approve again.

   ![Apex](/docs/assets/MCP/mcp-11.png)

   **7.** Finally, it provide the response and task completed message.

   ![Apex](/docs/assets/MCP/mcp-12.png)

   **8.** Now let me ask bit complex question from the DB, like **What are the Toyota models manufactured in 2022?**

   ![Apex](/docs/assets/MCP/mcp-13.png)

   **9.** Same like above steps , first it will ask approval to connect database using connect tool, Once I click approve , it will connect to database and ask to use **schema-information** tool, click approve

   ![Apex](/docs/assets/MCP/mcp-14.png)

   **10.** After that it will find the CAR table from schema information and ask us to click on Act to execute the query.

   ![Apex](/docs/assets/MCP/mcp-15.png)
    
   **11.** Click on Act and finally it will ask to approve the SQL before execute, Click Approve

   ![Apex](/docs/assets/MCP/mcp-16.png)

   **12.** Voila! we get the correct response, it's cool

   ![Apex](/docs/assets/MCP/mcp-17.png)
    
    

    
      
