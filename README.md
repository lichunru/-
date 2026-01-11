# 中医智能康养管理系统 (TCMWR)

## 项目概述

这是一个基于Spring Boot + Vue.js的全栈中医智能康养管理系统，集成DeepSeek V3大模型API，实现用户健康管理、数据采集、智能推荐、计划制定和数据可视化等核心功能。

## 技术架构

### 前端技术栈
- **框架**: Vue 3 + Composition API
- **构建工具**: Vite
- **UI组件库**: Element Plus
- **图表库**: ECharts 5.x
- **HTTP客户端**: Axios
- **状态管理**: Pinia
- **路由**: Vue Router 4

### 后端技术栈
- **框架**: Spring Boot 3.2.0
- **语言**: Java 17
- **安全框架**: Spring Security + OAuth2.0 + JWT
- **数据库**: MySQL 8.x
- **ORM**: MyBatis Plus + JPA
- **缓存**: Redis
- **API文档**: Swagger/OpenAPI 3

### AI集成
- **模型**: DeepSeek V3
- **API Key**: sk-bbc4d410ad284c13b4780fca63838583
- **功能**: 智能推荐、文本分析、知识库检索

## 项目结构

```
d:/TCMWR/
├── frontend/                    # 前端项目
│   ├── src/
│   │   ├── api/                # API接口封装
│   │   ├── components/         # 通用组件
│   │   ├── views/              # 页面组件
│   │   ├── store/              # Pinia状态管理
│   │   ├── router/             # 路由配置
│   │   ├── utils/              # 工具函数
│   │   └── assets/             # 静态资源
│   ├── package.json            # 依赖配置
│   └── vite.config.js          # Vite配置
│
├── backend/                     # 后端项目
│   ├── src/main/java/com/tcmwr/
│   │   ├── config/             # 配置类
│   │   ├── controller/         # 控制器层
│   │   ├── service/            # 服务层
│   │   ├── entity/             # 实体类
│   │   ├── mapper/             # 数据访问层
│   │   ├── dto/                # 数据传输对象
│   │   ├── utils/              # 工具类
│   │   └── exception/          # 异常处理
│   ├── src/main/resources/     # 资源文件
│   └── pom.xml                 # Maven配置
│
├── database/                    # 数据库脚本
│   ├── schema.sql              # 数据库结构
│   └── data.sql                # 初始数据
│
├── knowledge/                   # 知识库系统
│   ├── frontend/               # 知识库前端
│   └── backend/                # 知识库后端
│
└── PROJECT_SPECIFICATION.md    # 项目规格书
```

## 核心功能模块

### 1. 用户管理与健康档案模块
- 账户生命周期管理（注册、登录、状态管理）
- 全维度健康档案构建（体质辨识、西医体检、中医问诊、康养行为）

### 2. 多源健康数据采集模块
- 设备数据实时接入与分类处理
- 手动数据补充录入与校验

### 3. 中医智能康养服务推荐模块
- 健康数据比对与辨证分析
- 个性化康养服务推送（基于DeepSeek V3 + 知识库）

### 4. 健康管理计划制定模块
- 目标导向的计划生成
- 计划动态调整与进度追踪

### 5. 健康数据可视化与多维度分析模块
- 用户个人数据可视化（折线图、雷达图、热力图）
- 健康计划可视化（甘特图、进度条）

### 6. 登录注册模块
- OAuth2.0 + JWT 认证
- 注册页面（用户名、密码、确认密码）
- 登录页面（支持跳转到注册页面）

## 快速开始

### 环境要求
- Node.js 18.x+
- Java 17+
- MySQL 8.x
- Redis 6.x+
- Maven 3.8.x

### 启动步骤

#### 1. 数据库准备
```bash
# 创建数据库
mysql -u root -p
CREATE DATABASE tcmwr_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# 导入数据库结构
mysql -u root -p tcmwr_db < database/schema.sql
```

#### 2. 启动后端
```bash
cd backend
mvn clean install
mvn spring-boot:run
```

#### 3. 启动前端
```bash
cd frontend
npm install
npm run dev
```

#### 4. 访问系统
- 登录页面: http://localhost:3000/login
- 注册页面: http://localhost:3000/register
- API文档: http://localhost:8080/api/swagger-ui.html

## 配置说明

### 数据库配置
在 `backend/src/main/resources/application.yml` 中配置：
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/tcmwr_db
    username: root
    password: your_password
```

### Redis配置
```yaml
spring:
  data:
    redis:
      host: localhost
      port: 6379
      password: your_password
```

### DeepSeek API配置
```yaml
deepseek:
  api-key: sk-bbc4d410ad284c13b4780fca63838583
  base-url: https://api.deepseek.com
  model: deepseek-v3
```

## 安全特性

### 1. 认证授权
- OAuth2.0 + JWT 双重认证
- Token自动刷新机制
- 基于角色的访问控制（RBAC）

### 2. 数据加密
- AES-256 存储加密
- HTTPS + TLS 1.3 传输加密
- 密码哈希存储（BCrypt）

### 3. 安全防护
- 登录失败次数限制
- 异常登录检测
- 操作日志审计

## 数据库设计

### 核心表结构
- `users` - 用户基本信息
- `user_profiles` - 用户详细档案
- `health_records` - 健康档案汇总
- `device_data` - 设备采集数据
- `manual_data` - 手动录入数据
- `physical_constitution` - 体质辨识结果
- `recommendations` - 推荐结果
- `health_plans` - 健康计划
- `plan_tasks` - 计划任务
- `knowledge_base` - 知识库文档
- `knowledge_segments` - 知识库片段

## API接口规范

### 认证相关
```
POST /api/auth/register - 用户注册
POST /api/auth/login - 用户登录
POST /api/auth/refresh - Token刷新
POST /api/auth/logout - 用户登出
```

### 用户管理
```
GET /api/users/profile - 获取用户信息
PUT /api/users/profile - 更新用户信息
GET /api/users/health-record - 获取健康档案
POST /api/users/health-record - 更新健康档案
```

### 数据采集
```
POST /api/data/device - 设备数据接入
POST /api/data/manual - 手动数据录入
GET /api/data/history - 数据历史查询
POST /api/data/clean - 数据清洗
```

### 智能推荐
```
POST /api/recommend/analyze - 健康分析
GET /api/recommend/suggestions - 获取推荐
POST /api/recommend/feedback - 反馈收集
```

### 计划管理
```
POST /api/plan/create - 创建计划
GET /api/plan/list - 计划列表
PUT /api/plan/update - 更新计划
GET /api/plan/progress - 进度查询
```

### 数据分析
```
GET /api/analytics/trends - 趋势分析
GET /api/analytics/distribution - 分布分析
GET /api/analytics/correlation - 关联分析
POST /api/analytics/export - 数据导出
```

## 知识库系统

### 功能特性
- 文件上传（PDF、Word、TXT、Markdown）
- 智能解析（段落分割、语义提取）
- 向量化（文本向量生成、相似度计算）
- 检索引擎（关键词 + 语义检索）
- 管理界面（文档管理、标签管理、检索测试）

### 技术实现
- 文件解析：Apache POI + PDFBox
- 分词算法：Jieba分词 + 自定义词典
- 向量存储：FAISS / Chroma / Milvus
- 检索算法：BM25 + 语义相似度

## 性能指标

- **响应时间**: API平均响应 < 500ms
- **并发支持**: 支持1000+并发用户
- **数据处理**: 实时数据流处理能力
- **检索准确率**: 知识库检索 ≥85%
- **系统可用性**: 99.9% SLA

## 开发规范

### 代码规范
- Java: 阿里Java开发手册
- Vue: Vue Style Guide
- SQL: SQL编写规范
- Git: Git Flow工作流

### 提交规范
```
feat: 新功能
fix: 修复bug
docs: 文档更新
style: 代码格式调整
refactor: 代码重构
test: 测试相关
chore: 构建/工具相关
```

## 常见问题

### Q: 如何重置数据库？
A: 删除数据库后重新执行schema.sql

### Q: 前端无法连接后端？
A: 检查后端端口是否为8080，前端代理配置是否正确

### Q: Redis连接失败？
A: 确保Redis服务已启动，配置中的密码正确

### Q: DeepSeek API调用失败？
A: 检查API密钥是否有效，网络连接是否正常

## 联系方式

- 项目负责人: Cline AI Assistant
- 技术支持: 请查看项目文档
- 版本: v1.0
- 更新日期: 2026-01-04

## 许可证

本项目仅供学习和研究使用。
