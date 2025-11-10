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
- 用户认证和权限管理模块
- 实现AuthService类处理用户注册、登录、Token验证等核心功能
- 包含密码加密、Token生成与验证、用户信息管理等方法
- 提供init_auth_tables函数初始化认证相关的数据表结构
  
**3 database.py**  
- 数据库配置和操作核心模块
- 提供数据库连接配置和获取数据库连接的函数
- 负责初始化数据库表结构（会话表、消息表、图片表、附件表等）
- 实现SessionManager类管理会话的创建、获取、更新、删除等操作
- 包含MemoryDB类处理用户记忆和会话摘要的存储与检索

**4 mcp_client.py**  
- MCP（Model Control Protocol）客户端实现
- 通过stdio协议与本地MCP服务器进行通信
- 支持Python和Node.js类型的MCP服务器
- 实现MCPClient类处理与MCP服务器的具体通信逻辑
- 定义MCP服务器配置（fetch/time/git等）
- 实现MCPManager类管理多个MCP客户端实例

**5 rag_engine.py**  
- 检索增强生成（RAG）引擎实现
- 支持本地文档的向量化存储和高效检索
- 包含DocumentProcessor类处理文档读取（PDF/DOCX/TXT）和分块
- 实现XinferenceEmbedding类进行文本向量化处理
- RAGEngine类负责文档索引构建、增量更新和语义检索

**6 tools.py**  
- 工具定义和注册模块，为大模型提供工具调用能力
- 实现ToolRegistry类用于工具的注册和调用管理
- 注册了多种实用工具函数，如：
  - get_current_time：获取当前时间
  - calculate：执行数学计算
  - amap_*：高德地图相关功能（地理编码、逆地理编码、POI搜索）
  - fetch_*：网页内容获取和摘要生成
  - rag_search：基于本地知识库的检索
  - get_weather：天气查询
  - file操作：读取文件、列出目录内容
  - mcp_fetch：使用MCP服务抓取网页

