# Dbao（我们正在移除涉及公司内部资料的部分并用公有数据进行测试，代码将在测试完毕后上传）
在这里，我们搭建了一个Dbao大模型交互客户端，可以应用于企业的局域网连接，为企业数据隐私和大模型交互提供一个前端和后端交互框架。Dbao支持解析图像、视频和各种类型的文本文档。它还配备了上下文记忆，切换模型，各种mcp功能（如解析网页等），以构建企业专用的RAG知识库。  
Dbao可以给初步入门大模型开发的同学提供一定的思路，并且还可以在此基础上进行进一步完善。希望Dbao能够给你带来不一样的体验。注意：所有演示的数据都使用公开的的测试数据集，请勿泄露重要信息。祝好~
## 1 启动模型
为了方便大家快速上手，我们写了一个start.sh启动文件，大家只需要填写.env文件并且配置好对应的环境内容即可：  
<img width="627" height="854" alt="启动项" src="https://github.com/user-attachments/assets/6c33d5fb-7d57-43d8-8ca4-a3f055f458f6" />
## 2 注册和登陆
正式进入之前大家需要进行一个简单的注册：
<img width="508" height="718" alt="注册" src="https://github.com/user-attachments/assets/30399669-7ce3-4173-a2cc-d0e2b9a65b33" />
## 3 界面简介  
在这里，Dbao会自动记录同一用户的消息，并且启用了回溯功能，用户可以查看历史信息；并且如果您使用的是多模态模型，那么就可以上传图片，视频（会进行抽帧处理）和文本等文件；我们在右下角设置了暂停功能，方便用户聊天：
<img width="1856" height="945" alt="界面介绍" src="https://github.com/user-attachments/assets/a6c4865b-a7c5-4b75-a084-eb5b8b5b0096" />
## 4 工具调用
为了使大模型有更强大的功能，我们在里面部署了一些常用的工具（比如时间，地图，网页解析等）：  
<img width="1644" height="854" alt="工具调用" src="https://github.com/user-attachments/assets/a1419527-6d2f-4790-aeb0-a5d61963e07c" />
## 5 模型选择
Dbao会自动监测大模型端口，添加本地已经部署好的大模型，并且还可以添加我们购买的大模型接口：
<img width="1637" height="788" alt="模型选择" src="https://github.com/user-attachments/assets/95c39f6d-c54b-477f-a215-525ff4b18064" />
## 6 模型的记忆功能
在这里我们测试大模型的记忆功能，中途换模型也不会有影响：
<img width="1859" height="932" alt="记忆测试" src="https://github.com/user-attachments/assets/5294085b-a217-4d25-9f3c-ab71d9dc2dcf" />
<img width="1857" height="930" alt="记忆测试1" src="https://github.com/user-attachments/assets/4448d370-4981-4f2f-9175-7b625d06673c" />
## 7 多模态性能
我们可以同时上传图片，视频和文字文档给大模型一起处理：
<img width="1858" height="942" alt="0多文件测试" src="https://github.com/user-attachments/assets/95655a52-7d5b-4799-9992-b10d3306661a" />
<img width="1798" height="934" alt="1" src="https://github.com/user-attachments/assets/a656a95f-6d55-4e01-ba1a-cf936c4c0a01" />
## 8 markdown渲染
所有模型的输出都经历了渲染，使得更好看：
<img width="1875" height="990" alt="markdown渲染" src="https://github.com/user-attachments/assets/e768d403-99ff-44c1-a7b2-2d5b5e899d15" />
## 9 数据永久化存储
我们在后端使用sql数据库记录了所有用户的所有信息：
<img width="1380" height="899" alt="数据库" src="https://github.com/user-attachments/assets/c9d080b7-2c2a-403c-a5e0-fc85cf8d1207" />
## 10 调用工具
**1.OCR文档对比**  
我们只用输入两个文档进行对比即可：
<img width="1110" height="593" alt="图片" src="https://github.com/user-attachments/assets/66cf71af-ad26-4f8b-86c2-302edbb50f47" />  
**2.网站更新监测**  
<img width="705" height="589" alt="图片" src="https://github.com/user-attachments/assets/bb71257e-cc8a-4fa1-8df0-515151193be9" />  
  
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
- **.env**
- **database.py line22(SQL)**
- **main.py line104 112(LLM)**
- **rag_engine.py line122 202(embedding)**    

Finally, you just need to start the start.sh configuration file!  Let's start!  
