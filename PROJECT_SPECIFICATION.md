# 中医智能康养管理系统 - 项目技术规格书

## 项目概述

本项目是一个基于Spring Boot + Vue.js的全栈中医智能康养管理系统，集成DeepSeek V3大模型API，实现用户健康管理、数据采集、智能推荐、计划制定和数据可视化等核心功能。

## 技术架构

### 前端技术栈
- **框架**: Vue 3 + Composition API
- **构建工具**: Vite
- **UI组件库**: Element Plus
- **图表库**: ECharts 5.x
- **3D可视化**: Three.js (可选)
- **HTTP客户端**: Axios
- **状态管理**: Pinia
- **路由**: Vue Router 4

### 后端技术栈
- **框架**: Spring Boot 3.x
- **语言**: Java 17+
- **安全框架**: Spring Security + OAuth2.0 + JWT
- **数据库**: MySQL 8.x
- **ORM**: MyBatis Plus / JPA
- **缓存**: Redis (可选)
- **API文档**: Swagger/OpenAPI 3

### AI集成
- **模型**: DeepSeek V3
- **API认证**: API Key (sk-bbc4d410ad284c13b4780fca63838583)
- **功能**: 智能推荐、文本分析、知识库检索

## 项目目录结构

```
d:/TCMWR/
├── frontend/                    # 前端项目
│   ├── src/
│   │   ├── api/                # API接口封装
│   │   ├── components/         # 通用组件
│   │   ├── views/              # 页面组件
│   │   │   ├── Login.vue       # 登录页面
│   │   │   ├── Register.vue    # 注册页面
│   │   │   ├── Dashboard.vue   # 主仪表板
│   │   │   ├── UserManage.vue  # 用户管理模块
│   │   │   ├── HealthData.vue  # 健康数据采集模块
│   │   │   ├── SmartRec.vue    # 智能推荐模块
│   │   │   ├── PlanManage.vue  # 计划管理模块
│   │   │   └── Analytics.vue   # 数据可视化模块
│   │   ├── store/              # Pinia状态管理
│   │   ├── router/             # 路由配置
│   │   ├── utils/              # 工具函数
│   │   ├── assets/             # 静态资源
│   │   └── App.vue             # 根组件
│   ├── public/                 # 静态文件
│   ├── index.html              # HTML入口
│   ├── package.json            # 依赖配置
│   ├── vite.config.js          # Vite配置
│   └── tsconfig.json           # TypeScript配置
│
├── backend/                     # 后端项目
│   ├── src/main/java/com/tcmwr/
│   │   ├── TcmwrApplication.java          # Spring Boot启动类
│   │   ├── config/                        # 配置类
│   │   │   ├── SecurityConfig.java        # 安全配置
│   │   │   ├── JwtConfig.java             # JWT配置
│   │   │   ├── OAuth2Config.java          # OAuth2配置
│   │   │   └── SwaggerConfig.java         # API文档配置
│   │   ├── controller/                    # 控制器层
│   │   │   ├── AuthController.java        # 认证控制器
│   │   │   ├── UserController.java        # 用户管理控制器
│   │   │   ├── HealthDataController.java  # 健康数据控制器
│   │   │   ├── RecommendController.java   # 智能推荐控制器
│   │   │   ├── PlanController.java        # 计划管理控制器
│   │   │   └── AnalyticsController.java   # 数据分析控制器
│   │   ├── service/                       # 服务层
│   │   │   ├── impl/                      # 服务实现
│   │   │   │   ├── AuthServiceImpl.java
│   │   │   │   ├── UserServiceImpl.java
│   │   │   │   ├── HealthDataServiceImpl.java
│   │   │   │   ├── RecommendServiceImpl.java
│   │   │   │   ├── PlanServiceImpl.java
│   │   │   │   └── AnalyticsServiceImpl.java
│   │   │   └── interfaces/                # 服务接口
│   │   ├── entity/                        # 实体类
│   │   │   ├── User.java                  # 用户实体
│   │   │   ├── HealthRecord.java          # 健康档案
│   │   │   ├── DeviceData.java            # 设备数据
│   │   │   ├── ManualData.java            # 手动数据
│   │   │   ├── HealthPlan.java            # 健康计划
│   │   │   └── Recommendation.java        # 推荐结果
│   │   ├── mapper/                        # 数据访问层
│   │   │   ├── UserMapper.java
│   │   │   ├── HealthDataMapper.java
│   │   │   └── PlanMapper.java
│   │   ├── dto/                           # 数据传输对象
│   │   │   ├── request/                   # 请求DTO
│   │   │   └── response/                  # 响应DTO
│   │   ├── utils/                         # 工具类
│   │   │   ├── JwtUtils.java              # JWT工具
│   │   │   ├── CryptoUtils.java           # 加密工具
│   │   │   ├── DeepSeekClient.java        # DeepSeek客户端
│   │   │   └── DataCleanUtils.java        # 数据清洗工具
│   │   └── exception/                     # 异常处理
│   ├── src/main/resources/
│   │   ├── application.yml                # 主配置
│   │   ├── application-dev.yml            # 开发配置
│   │   ├── application-prod.yml           # 生产配置
│   │   ├── mapper/                        # MyBatis映射文件
│   │   ├── static/                        # 静态资源
│   │   └── templates/                     # 模板文件
│   ├── pom.xml                            # Maven配置
│   └── Dockerfile                         # Docker配置
│
├── database/                      # 数据库脚本
│   ├── schema.sql                 # 数据库结构
│   ├── data.sql                   # 初始数据
│   ├── procedures.sql             # 存储过程
│   └── views.sql                  # 视图定义
│
└── knowledge/                     # 知识库系统 (独立项目)
    ├── frontend/                  # 知识库前端
    │   ├── src/
    │   │   ├── views/
    │   │   │   ├── Upload.vue     # 文件上传
    │   │   │   ├── Search.vue     # 知识检索
    │   │   │   └── Manage.vue     # 知识管理
    │   │   └── api/
    │   │       └── knowledge.js   # 知识库API
    │   └── package.json
    │
    └── backend/                   # 知识库后端
        ├── src/main/java/com/knowledge/
        │   ├── controller/
        │   │   └── KnowledgeController.java
        │   ├── service/
        │   │   └── KnowledgeService.java
        │   ├── entity/
        │   │   ├── KnowledgeDoc.java    # 知识文档
        │   │   └── KnowledgeSegment.java # 文档片段
        │   ├── utils/
        │   │   ├── FileParser.java      # 文件解析器
        │   │   └── VectorSearch.java    # 向量检索
        │   └── TcmKnowledgeApplication.java
        ├── src/main/resources/
        │   └── application.yml
        └── pom.xml
```

## 核心功能模块

### 1. 用户管理与健康档案模块

#### 1.1 账户生命周期管理
- **注册认证**: 用户名、密码（二次确认）、基础信息录入
- **登录管理**: 多维度登录（用户名/手机号/邮箱）、状态管理
- **信息维护**: 在线编辑、提交验证、完整性检查

#### 1.2 全维度健康档案构建
- **数据整合**: 体质辨识、西医体检、中医问诊、康养行为
- **标准化处理**: 数据清洗、格式统一、异常值处理
- **动态更新**: 实时同步、版本管理、历史追溯

### 2. 多源健康数据采集模块

#### 2.1 设备数据实时接入
- **协议适配**: 智能穿戴设备、中医检测设备
- **实时采集**: WebSocket长连接、数据流处理
- **自动分类**: 生理指标分类、异常检测
- **结构化存储**: 数据库规范化存储

#### 2.2 手动数据补充录入
- **结构化表单**: 动态表单生成、必填项验证
- **非结构化上传**: 文本、图片、文档上传
- **实时校验**: 格式验证、逻辑校验、完整性检查
- **数据同步**: 与设备数据合并、更新档案

### 3. 中医智能康养服务推荐模块

#### 3.1 健康数据比对与辨证分析
- **标准库建设**: 西医指标范围、中医体质阈值
- **多维度比对**: 异常项识别、趋势分析
- **辨证模型**: 体质-证候-病机关联模型
- **智能报告**: 辨证结果、健康评估、风险预警

#### 3.2 个性化康养服务推送
- **DeepSeek集成**: 调用V3模型进行智能分析
- **知识库检索**: 在knowledge库中进行相关度匹配（≥85%准确率）
- **方案生成**: 食疗方、中药茶饮、经络穴位、养生功法
- **推送策略**: 科普知识、康养建议、干预方案

### 4. 健康管理计划制定模块

#### 4.1 目标导向的计划生成
- **目标定义**: 用户自定义健康目标
- **任务拆解**: 阶段性任务、时间节点、执行要求
- **可视化计划**: 日程表、甘特图、任务清单

#### 4.2 计划动态调整与进度追踪
- **状态监控**: 健康数据同步、执行偏差检测
- **自动调整**: 任务优化、时间重排、内容更新
- **进度看板**: 完成率、趋势图、依从性分析

### 5. 健康数据可视化与多维度分析模块

#### 5.1 用户个人数据可视化
- **趋势图表**: 折线图（生理指标趋势）
- **分布分析**: 雷达图（体质评分）
- **关联关系**: 热力图（症状关联）
- **数据导出**: CSV、Excel、PDF格式

#### 5.2 健康计划可视化
- **进度展示**: 甘特图（计划执行）
- **完成情况**: 进度条、环形图
- **效果评估**: 前后对比、达成率

### 6. 登录注册模块

#### 6.1 OAuth2.0 + JWT 认证
- **认证流程**: OAuth2授权码模式
- **JWT生成**: Token签发、刷新机制
- **安全策略**: HTTPS传输、AES-256存储加密

#### 6.2 注册页面
- **字段要求**: 用户名、密码、确认密码
- **验证逻辑**: 用户名唯一性、密码强度、一致性校验
- **交互设计**: 实时反馈、错误提示、成功跳转

#### 6.3 登录页面
- **登录方式**: 用户名/手机号/邮箱
- **安全特性**: 验证码、记住登录、异常检测
- **页面跳转**: 注册页面链接、忘记密码

## 核心技术实现

### 1. 双模式数据采集
- **智能设备接入**: WebSocket + MQTT协议
- **手动表单**: 动态Schema + 表单引擎
- **数据清洗**: 异常值过滤、缺失值补全、格式标准化
- **质量控制**: 数据验证、完整性检查、一致性校验

### 2. 中医智能推荐
- **知识库构建**: 国标体质辨识标准、诊疗指南
- **检索算法**: 语义相似度 + 关键词匹配
- **大模型集成**: DeepSeek V3 API调用
- **准确率目标**: ≥85%的相关度匹配

### 3. 数据可视化
- **图表库**: ECharts 5.x（2D）+ Three.js（3D）
- **图表类型**: 
  - 趋势图：折线图、面积图
  - 分布图：雷达图、柱状图
  - 关联图：热力图、桑基图
  - 进度图：甘特图、进度环
- **交互功能**: 缩放、筛选、导出

### 4. 安全加密
- **传输安全**: HTTPS + TLS 1.3
- **存储加密**: AES-256加密敏感数据
- **认证授权**: OAuth2.0 + JWT + RBAC
- **安全审计**: 日志记录、异常监控

### 5. 个性化计划
- **可视化编辑**: 拖拽式计划编辑器
- **动态调整**: 规则引擎 + AI优化
- **进度追踪**: 实时同步、偏差预警
- **效果评估**: 多维度指标分析

## 数据库设计

### 核心表结构

#### 用户相关
- `users` - 用户基本信息
- `user_profiles` - 用户详细档案
- `health_records` - 健康档案汇总
- `auth_logs` - 认证日志

#### 数据采集
- `device_data` - 设备采集数据
- `manual_data` - 手动录入数据
- `data_sources` - 数据源配置
- `data_quality` - 数据质量记录

#### 健康分析
- `physical_constitution` - 体质辨识结果
- `symptom_records` - 症状记录
- `diagnosis_records` - 诊断记录
- `health_indicators` - 健康指标

#### 推荐与计划
- `recommendations` - 推荐结果
- `health_plans` - 健康计划
- `plan_tasks` - 计划任务
- `task_executions` - 任务执行记录

#### 知识库
- `knowledge_base` - 知识文档
- `knowledge_segments` - 文档片段
- `knowledge_tags` - 标签体系
- `search_history` - 搜索历史

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

## 知识库系统 (d:/knowledge)

### 功能特性
- **文件上传**: 支持PDF、Word、TXT、Markdown
- **智能解析**: 段落分割、语义提取
- **向量化**: 文本向量生成、相似度计算
- **检索引擎**: 关键词 + 语义检索
- **管理界面**: 文档管理、标签管理、检索测试

### 技术实现
- **文件解析**: Apache POI + PDFBox
- **分词算法**: Jieba分词 + 自定义词典
- **向量存储**: FAISS / Chroma / Milvus
- **检索算法**: BM25 + 语义相似度
- **API接口**: RESTful + WebSocket

## 部署与运维

### 开发环境
- **Node.js**: 18.x+
- **Java**: 17+
- **MySQL**: 8.x
- **Maven**: 3.8.x
- **Vite**: 4.x

### 生产环境
- **Web服务器**: Nginx
- **应用服务器**: Tomcat / Spring Boot内嵌
- **数据库**: MySQL主从复制
- **缓存**: Redis集群
- **监控**: Prometheus + Grafana

### CI/CD
- **代码管理**: Git
- **构建工具**: Jenkins / GitHub Actions
- **容器化**: Docker + Docker Compose
- **部署策略**: 蓝绿部署 / 滚动更新

## 性能指标

- **响应时间**: API平均响应 < 500ms
- **并发支持**: 支持1000+并发用户
- **数据处理**: 实时数据流处理能力
- **检索准确率**: 知识库检索 ≥85%
- **系统可用性**: 99.9% SLA

## 安全要求

- **认证**: OAuth2.0 + JWT
- **加密**: AES-256存储加密
- **传输**: HTTPS + TLS 1.3
- **权限**: RBAC访问控制
- **审计**: 操作日志 + 安全审计

## 开发规范

### 代码规范
- **Java**: 阿里Java开发手册
- **Vue**: Vue Style Guide
- **SQL**: SQL编写规范
- **Git**: Git Flow工作流

### 文档规范
- **API文档**: Swagger/OpenAPI
- **代码注释**: Javadoc + JSDoc
- **技术文档**: Markdown格式
- **提交信息**: Conventional Commits

### 测试规范
- **单元测试**: JUnit + Jest
- **集成测试**: Testcontainers
- **API测试**: Postman + Newman
- **E2E测试**: Cypress / Playwright

---

**版本**: v1.0  
**创建日期**: 2026-01-04  
**技术负责人**: Cline AI Assistant  
**状态**: 规划阶段
