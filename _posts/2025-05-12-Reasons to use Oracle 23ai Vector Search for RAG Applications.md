## Reasons to Use Oracle 23ai Vector Search for RAG Applications

![Apex](/docs/assets/images/vector.PNG)

**RAG (Retrieval-augmented generation)** is a technique that can provide more accurate results to queries than a generative LLM on its own because RAG uses knowledge external to data already contained in LLM.

**Oracle AI Vector Search** is an innovative feature introduced in Oracle Database 23c that enhances data retrieval capabilities. This functionality enables users to search for AI vectors directly within the database, streamlining the process of accessing complex data types. 


### Benefits:

**1. Vectors as a Native Data Type**

Oracle Database 23ai introduces the ability to store both relational and vector data. This integration allows users to combine traditional relational queries with similarity searches that are based on semantic content. 

By incorporating AI vector search into Oracle Database, Oracle enables customers to leverage the advantages of artificial intelligence while maintaining security, data integrity, and performance.


**2. Coding Language**

Oracle developers and database administrators (DBAs) can now create complete Retrieval-Augmented Generation (RAG) applications using only SQL and PL/SQL, eliminating the need to learn new programming languages like Python or rely on open-source libraries such as LangChain. This solution enables users to effectively load, vectorize, search, and analyze questions about document content, all while leveraging the capabilities of familiar Oracle tools. This approach simplifies the development process, enhances productivity, and reduces the complexity associated with adopting new technologies.

**3. Specialized Vector Database**

Clients won't need to invest extra money in training database administrators or developers to learn a specialized vector database. There’s no requirement to transfer data into a specialized vector database. Instead, your team can concentrate on enhancing a large language model (LLM) with company data. This approach helps you avoid data synchronization issues and the complexity of managing multiple products, ultimately saving on additional costs.


**4. Security of Data**

We can now convert pre-trained transformer models from Hugging Face into the ONNX (Open Neural Network Exchange) format. This format can be imported into 23ai to generate vector embeddings. This approach ensures that no data is transmitted outside the database, making the process more secure and quicker, as there are no API calls made over the internet.
