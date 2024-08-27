## How to use APEX Assistant (AI chat capability) :robot:

### Introduction:
APEX Assistant adds AI chat capability to all APEX code editors to assist you with writing SQL queries, debugging code, and so on.

### Pre-Requisite:
Before you can use APEX Assistant, you must create an Generative AI Service and enable the **Used by App Builder** setting.
see my last blog post [how to configure Gen AI service in Oracle APEX using Open AI](https://mksingla.github.io/2024/08/26/How-to-configure-Gen-AI-service-in-Oracle-APEX-using-OpenAI.html)

To use APEX Assistant, Login to Apex workspace --> Go to the SQL Workshop -> go to SQL Commands and click on APEX Assistent. See my above blog post.

Here you will see APEX Assistnat have 2 menu options:

- **Query Builder** - Use Query Builder to get back a simple query.

  In Query Builder mode, the AI assumes all questions are in the context of the customer schema in the database. For example, if your request that the AI create SQL for tables that do not exist in the database, APEX 
  Assistant's responses will not be very helpful.

- **General Assistance** - Use General Assistance for general conversation, technical questions such as "Explain this" or "Improve this code." In General Assistance mode, APEX Assistant prompts you with default options such 
  as **Use Selection, Improve Selection, and Explain Selection**.

Let's see how Query Builder works.
  
  1. From the menu, select Query builder.
  2. In code editor, select the query and click **Use Selection**.
  3. You will see the query is APEX wizard.


  4.   In Type your mesage here, enter show average salary of employee by department name and click send message.
 

  5. APEX Assistnat responds with a query. This is amazing!
 

  6. Here you can **copy or insert** to copy or insert the response into Code Editor. I click **insert** and you can see the code in Code Editor.
  7. Now you can **Run** this code to get the result as well if you have this table in your schema.


  8. I would like to show you another best feature of APEX assistent which is Chat Widget memory (the context of the chat). For example, I asked how many belongs to department, Given the context in the chat, it already 
     know I am talking about employee. This is great!


  9. Now click **Clear Chat**.






     
