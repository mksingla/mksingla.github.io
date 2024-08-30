## How to use APEX Assistant (AI chat capability) 🤖

### Introduction:
APEX Assistant adds AI chat capability to all APEX code editors to assist you with writing SQL queries, debugging code, and so on.

### Pre-Requisite:
Before you can use APEX Assistant, you must create an Generative AI Service and enable the **Used by App Builder** setting.
see my last blog post [how to configure Gen AI service in Oracle APEX using Open AI](https://mksingla.github.io/2024/08/26/How-to-configure-Gen-AI-service-in-Oracle-APEX-using-OpenAI.html)

To use APEX Assistant, Login to Apex workspace --> Go to the SQL Workshop -> go to SQL Commands and click on APEX Assistent. See my above blog post.

  ![Apex](/docs/assets/apex_assistant/step1-1.PNG)

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
   
       ![Apex](/docs/assets/apex_assistant/step1-2.PNG)

  4.   In Type your mesage here, enter show average salary of employee by department name and click send message.
 
       ![Apex](/docs/assets/apex_assistant/step1-3.PNG)
       
  6. APEX Assistnat responds with a query. This is amazing!

       ![Apex](/docs/assets/apex_assistant/step1-4.PNG)

  8. Here you can **copy or insert** to copy or insert the response into Code Editor. I click **insert** and you can see the code in Code Editor.
  9. Now you can **Run** this code to get the result as well if you have this table in your schema.

       ![Apex](/docs/assets/apex_assistant/step1-5.PNG)

  10. I would like to show you another best feature of APEX assistent which is Chat Widget memory (the context of the chat). For example, I asked how many belongs to department, Given the context in the chat, it already 
     know I am talking about employee. This is great!

       ![Apex](/docs/assets/apex_assistant/step1-6.PNG)

  11. Now click **Clear Chat**.

Now Let's see how General Assistance works:

  1. From the menu, select General Assistance
  2. Apex Assistant displays three options:
     **- Use selection**
     **- Improve selection**
     **- Explain selection**

  ![Apex](/docs/assets/apex_assistant/step2-1.PNG)
    
  4. In the Code Editor, select the query and click **Explain selection**. APEX Assistant describe the query.

  ![Apex](/docs/assets/apex_assistant/step2-2.PNG)

  5. Click **Clear Chat** to clear the chat windows.
  6. Next, I select the query and click on **Use selection**, APEX Assistant respond with **how can I assist you with it?**

  ![Apex](/docs/assets/apex_assistant/step2-3.PNG)

  7. Now I click on Improve and assistant improved the query and specify what improvements made.

  ![Apex](/docs/assets/apex_assistant/step3-3.PNG)
  
  8. Now let me test one more thing, by purpose I made a mistake and i removed semicolon after manager and use below query and then select Imrpove selection.

   ```
SELECT ID,
     firstname,
     lastname,
     COUNTRY,
     email,
     position,
     manager
     GENDER
FROM customer
WHERE country = 'INDIA'
```
APEX assistant Improve the query and also correct the query.

![Apex](/docs/assets/apex_assistant/step2-4.PNG)

 8. Again, clear the chat.

So you can see how interesting is this APEX Assistant which can help in query generation, query correction and query Improvement.      

     
   




     
