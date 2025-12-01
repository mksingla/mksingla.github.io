## SQL Notebooks in Oracle SQL Developer extension for VS Code


### Introduction:
SQL Notebook is a powerful feature of the SQL Developer Extension for VS Code that offers an alternative to SQL Worksheets that build up a series of queries with Markdown, similar to user defined reports.
It works the same way as Jupyter notebook to execute python code.

### Pre-Requisite:
SQL Developer extension for VS Code installed and connected with Oracle database.
See my last blog post [Connect to Oracle Database with VS Code using SQL Developer Extension and SQLcl](https://mksingla.github.io/2025/11/27/Install-SQL-Developer-Extension-for-VS-Code-and-SQLcl.html)

### Work with SQL Notebook

Right click on your connection and click **Open SQL Notebook**

It will open SQL Notebook into a new editor with unsaved **.sqlnb file**. Looks similar to Jupyter notebook.




SQL notebook features:
1. Code completion:


2.  We can generate query using "Generate" feature in SQL notebook by using natural language.

    Click on Generate and ask any question relted to DB (If you see, it is using GPT-5 mini) model.

    Once we get the rsponse , Click Accept

    Now run the query

3. Another feature in Markdown
   Click on Markdown and a markdown cell will create

   Now write comment or description and click on the rigth symbol

4. Also, we can run any select statement and the output in grid form, which is easy to read.

   
   
   
