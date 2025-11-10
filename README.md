# Dbao
Here, we have built a similar Dbao large model interaction client, which can be applied to the local area network connection of enterprises and provide a front-end and back-end interaction framework for enterprise data privacy and large model interaction.  
## Function Introduction
The Dbao framework supports parsing images, videos, and various types of text documents. It is also equipped with context memory and various mcp functions (such as parsing web pages, etc.) to build an enterprise-specific RAG knowledge base.  
<img width="1844" height="946" alt="1" src="https://github.com/user-attachments/assets/989f57da-19fb-4ece-94f9-cbb689b9b01d" />  
Each user can define their own account  
<img width="490" height="705" alt="2" src="https://github.com/user-attachments/assets/477e183f-232f-4458-9769-8b4dbeb1798a" />  
The user's data will be saved in the sql database  
<img width="1438" height="1010" alt="3" src="https://github.com/user-attachments/assets/6455ba71-a023-4eff-ab22-a40183a01d1c" />  

## Introduction to Code Files
**1 main.py** 
- The main entry point of the application, a web service built on FastAPI
- Responsible for initializing database connections, authentication tables, and CORS configuration
- Configure the OpenAI client to connect to the Tongyi Qianwen model service
- Implement session management functionality and multimodal processing capabilities
- Define utility functions such as PDF/DOCX text extraction and video frame extraction
- Provide API endpoints for interaction with the frontend 

**2 auth.py**  
- User authentication and permission management module
- Implement the AuthService class to handle core functions such as user registration, login, and Token verification
- Include methods for password encryption, Token generation and verification, user information management, etc.
- Provide the init_auth_tables function to initialize the structure of authentication-related data tables
  
**3 database.py**  
- Database configuration and core operation module
- Provide database connection configuration and functions for obtaining database connections
- Responsible for initializing database table structures (session table, message table, image table, attachment table, etc.)
- Implement the SessionManager class to manage operations such as session creation, retrieval, update, and deletion
- Include the MemoryDB class to handle the storage and retrieval of user memory and session summaries

**4 mcp_client.py**  
- MCP (Model Control Protocol) client implementation
- Communicate with the local MCP server via the stdio protocol
- Support Python and Node.js type MCP servers
- Implement the MCPClient class to handle specific communication logic with the MCP server
- Define MCP server configurations (fetch/time/git, etc.)
- Implement the MCPManager class to manage multiple MCP client instances

**5 rag_engine.py**  
- Retrieval-Augmented Generation (RAG) engine implementation
- Support vectorized storage and efficient retrieval of local documents
- Include the DocumentProcessor class to handle document reading (PDF/DOCX/TXT) and chunking
- Implement the XinferenceEmbedding class for text vectorization processing
- The RAGEngine class is responsible for document index construction, incremental updates, and semantic retrieval

**6 tools.py**  
- Tool definition and registration module, providing tool calling capabilities for large language models
- Implement the ToolRegistry class for tool registration and call management
- Register a variety of practical tool functions, such as:
  - get_current_time: Get the current time
  - calculate: Perform mathematical calculations
  - amap_*: Amap-related functions (geocoding, reverse geocoding, POI search)
  - fetch_*: Web content acquisition and summary generation
  - rag_search: Retrieval based on local knowledge base
  - get_weather: Weather query
  - File operations: Read files, list directory contents
  - mcp_fetch: Crawl web pages using MCP service

## Quick start 
First, you need to install the corresponding python module on your linux server according to requirements.txt.  
Then you need to modify the account and password corresponding to your own large model and database:
- .env
- database.py line22
- main.py line104 108 112  
Finally, you just need to start the start.sh configuration file!  
<img width="1849" height="943" alt="4" src="https://github.com/user-attachments/assets/8c5d129b-d66a-4b03-ab1b-369aacb43aca" />  
<img width="1866" height="922" alt="5" src="https://github.com/user-attachments/assets/a24b9e67-f425-4344-81a1-d2c9e8b324b9" />

