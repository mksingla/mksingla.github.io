## SQL Notebooks in Oracle SQL Developer extension for VS Code


### Introduction:
SQL Notebook is a powerful feature of the SQL Developer Extension for VS Code that offers an alternative to SQL Worksheets that build up a series of queries with Markdown, similar to user defined reports.
It works the same way as Jupyter notebook to execute python code.

### Pre-Requisite:
SQL Developer extension for VS Code installed and connected with Oracle database.
See my last blog post [Connect to Oracle Database with VS Code using SQL Developer Extension and SQLcl](https://mksingla.github.io/2025/11/27/Install-SQL-Developer-Extension-for-VS-Code-and-SQLcl.html)

### Work with SQL Notebook

Right click on your connection and click **Open SQL Notebook**

 ![Apex](/docs/assets/images/nb-1.png)  

It will open SQL Notebook into a new editor with unsaved **.sqlnb file**. Looks similar to Jupyter notebook.

 ![Apex](/docs/assets/images/nb-2.png)  


**SQL notebook features:**

**1. Code completion feature:**

 ![Apex](/docs/assets/images/nb-3.png)  
 
 ![Apex](/docs/assets/images/nb-4.png) 
 
**2.  Generate Query**

We can generate query using **"Generate"** feature in SQL notebook by using natural language.

Click on Generate and ask any question related to DB (If you see, it is using GPT-5 mini) model.

![Apex](/docs/assets/images/nb-5.png)  

   Once we get the response, Click Accept

![Apex](/docs/assets/images/nb-6.png) 

    Now run the query

![Apex](/docs/assets/images/nb-7.png) 

**3. Another feature is Markdown**
   Click on Markdown and a markdown cell will create

![Apex](/docs/assets/images/nb-8.png) 

   Now write comment or description and click on the right check symbol

![Apex](/docs/assets/images/nb-9.png) 

![Apex](/docs/assets/images/nb-10.png) 

**4. Also, we can run any select statement and the output is shown in grid form, which is easy to read.**

![Apex](/docs/assets/images/nb-11.png) 

   
   
   
