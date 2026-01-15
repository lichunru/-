# 中医智能康养管理系统 (TCMWR)

## 🎯 项目概述

这是一个现代化的中医智能康养管理系统，基于 **Spring Boot 3.5.9** + **Vue.js 3** + **MySQL 8.0** 构建。系统提供用户管理、健康数据监测、智能推荐、健康计划、知识库等完整功能，集成 **DeepSeek AI** 提供智能化健康建议。

## 🚀 当前状态

✅ **部署完成** - 系统已成功部署并运行

- **后端服务**: http://localhost:8081/api
- **前端服务**: http://localhost:5174/
- **数据库**: MySQL 8.0 (tcmwr_db)
- **状态**: 运行正常

## 🏗️ 技术架构

### 后端技术栈
- **Spring Boot 3.5.9** - 核心框架
- **Spring Security** - 安全认证
- **MyBatis** - ORM框架
- **MySQL 8.0** - 主数据库
- **JWT** - 身份认证
- **DeepSeek API** - AI智能推荐

### 前端技术栈
- **Vue.js 3** - 前端框架
- **Vite** - 构建工具
- **Element Plus** - UI组件库
- **Pinia** - 状态管理
- **Axios** - HTTP客户端

## 📁 项目结构

```
TCMWR/
├── backend/                    # 后端代码
│   ├── src/main/java/com/tcmwr/
│   │   ├── config/            # 配置类
│   │   ├── controller/        # 控制器
│   │   ├── service/           # 业务逻辑
│   │   ├── entity/            # 实体类
│   │   └── utils/             # 工具类
│   ├── src/main/resources/    # 资源文件
│   └── pom.xml                # Maven配置
├── frontend/                  # 前端代码
│   ├── src/
│   │   ├── api/              # API接口
│   │   ├── store/            # 状态管理
│   │   ├── router/           # 路由配置
│   │   ├── utils/            # 工具类
│   │   └── views/            # 页面组件
│   └── package.json          # 依赖配置
├── 部署说明.md                # 详细部署文档
├── 快速使用指南.md            # 用户使用指南
└── README.md                 # 本文件
```

## 🎯 核心功能

### 1. 用户管理
- ✅ 用户注册/登录
- ✅ JWT认证
- ✅ 角色权限管理 (ADMIN/USER)

### 2. 健康数据管理
- ✅ 身体指标记录 (身高、体重、血压、血糖等)
- ✅ 健康档案管理
- ✅ 数据可视化展示

### 3. 健康计划
- ✅ 个性化健康计划制定
- ✅ 计划进度跟踪
- ✅ 状态管理

### 4. 智能推荐
- ✅ AI健康建议 (DeepSeek)
- ✅ 个性化推荐
- ✅ 饮食运动方案

### 5. 知识库
- ✅ 中医健康知识
- ✅ 文档管理
- ✅ 智能搜索

### 6. 健康报告
- ✅ AI分析报告
- ✅ 数据导出
- ✅ 趋势分析

## 🚀 快速开始

### 环境要求
- **JDK**: 17+
- **Node.js**: 18+
- **MySQL**: 8.0+
- **Maven**: 3.6+

### 启动服务

#### 1. 启动后端
```bash
cd backend
java -jar target/tcmwr-backend-1.0.0.jar
```

#### 2. 启动前端
```bash
cd frontend
npm run dev
```

#### 3. 访问系统
- **前端**: http://localhost:5174/
- **后端API**: http://localhost:8081/api
- **API文档**: http://localhost:8081/api/swagger-ui.html

### 默认管理员
```
用户名: admin
密码: 请通过注册页面创建
角色: ADMIN
```

## 📋 API接口示例

### 用户认证
```http
# 注册
POST /api/auth/register
{
  "username": "user123",
  "password": "password123",
  "email": "user@example.com"
}

# 登录
POST /api/auth/login
{
  "username": "user123",
  "password": "password123"
}
# 返回: JWT Token
```

### 健康数据
```http
# 添加健康数据
POST /api/health-data
Authorization: Bearer <token>
{
  "dataType": "血压",
  "value": "120/80",
  "unit": "mmHg"
}

# 获取健康数据
GET /api/health-data?dataType=血压&page=1&size=10
Authorization: Bearer <token>
```

### 智能推荐
```http
# 获取AI健康建议
POST /api/recommendation/health-advice
Authorization: Bearer <token>

# 返回: 个性化健康建议
```

## 🔧 配置说明

### 数据库配置 (application.yml)
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/tcmwr_db?useSSL=false&serverTimezone=Asia/Shanghai
    username: root
    password: 521314
    driver-class-name: com.mysql.cj.jdbc.Driver
```

### 前端代理 (vite.config.js)
```javascript
proxy: {
  '/api': {
    target: 'http://localhost:8081/api',
    changeOrigin: true,
    rewrite: (path) => path.replace(/^\/api/, '')
  }
}
```

## 📚 详细文档

- **部署说明**: 查看 `部署说明.md` 获取完整部署指南
- **使用指南**: 查看 `快速使用指南.md` 了解系统功能
- **API文档**: 访问 http://localhost:8081/api/swagger-ui.html

## 🛠️ 开发工具

### 后端开发
```bash
# 编译打包
cd backend
mvn clean package -DskipTests

# 运行测试
mvn test

# 查看依赖
mvn dependency:tree
```

### 前端开发
```bash
# 安装依赖
cd frontend
npm install

# 开发模式
npm run dev

# 构建生产版本
npm run build

# 代码检查
npm run lint
```

## 🔒 安全特性

- ✅ **JWT认证**: 无状态令牌认证
- ✅ **密码加密**: BCrypt加密存储
- ✅ **角色权限**: 基于角色的访问控制
- ✅ **数据隔离**: 用户数据严格隔离
- ✅ **CORS配置**: 安全的跨域策略

## 📊 数据库表结构

主要数据表：
- `users` - 用户表
- `health_data` - 健康数据表
- `health_records` - 健康档案表
- `health_plans` - 健康计划表
- `recommendations` - 推荐表
- `knowledge_base` - 知识库表
- `diagnosis` - 诊断记录表

## 🎨 系统特性

### 现代化UI
- 响应式设计，支持移动端
- Element Plus组件库
- 数据可视化图表
- 优雅的交互体验

### AI智能
- DeepSeek大模型集成
- 个性化健康建议
- 智能数据分析
- 自然语言处理

### 高性能
- Redis缓存优化
- 数据库连接池
- 异步处理
- 资源压缩

## 🐛 常见问题

### Q: 无法连接数据库？
A: 检查MySQL服务是否启动，确认数据库配置正确

### Q: 前端无法访问？
A: 确认Vite开发服务器已启动，检查端口是否被占用

### Q: API请求失败？
A: 检查后端服务状态，确认代理配置正确

## 🤝 贡献指南

1. Fork 项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 🙏 致谢

- **Spring Boot** - 强大的后端框架
- **Vue.js** - 优秀的前端框架
- **Element Plus** - 精美的UI组件
- **DeepSeek** - AI智能支持

## 📞 联系方式

如有问题或建议，请通过以下方式联系：
- **项目地址**: https://github.com/your-repo/tcmwr
- **文档地址**: https://docs.tcmwr.com

---

**版本**: v1.0.0  
**部署时间**: 2026-01-14  
**系统状态**: ✅ 运行正常  
**最后更新**: 2026-01-14
