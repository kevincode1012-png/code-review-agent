# CodeGuardian AI - 代码审查AI Agent

## 项目简介

CodeGuardian AI 是一个基于 Spring Boot 3.x 和 Java 21 的智能代码审查系统。它能够自动化地对代码进行深度审查，识别潜在的bug、安全漏洞、性能问题和代码异味，并生成详细的审查报告。

## 技术栈

- **Java**: 21
- **Spring Boot**: 3.2.0
- **数据库**: PostgreSQL
- **构建工具**: Maven
- **其他**: Lombok, Jackson, OkHttp, JavaParser, Thymeleaf

## 核心功能

- ✅ 代码片段审查
- ✅ 单个文件审查
- ✅ 目录审查
- ✅ 项目审查
- ✅ Git项目审查
- ✅ AI模型集成
- ✅ 审查报告生成（HTML/Markdown）
- ✅ 审查历史查询

## 快速开始

### 1. 环境要求

- JDK 21+
- Maven 3.6+

### 2. 配置AI服务（可选）

如果需要使用AI功能，需要配置AI服务：

```yaml
# application.yml
ai:
  base-url: https://api.openai.com
  api-key: your-api-key
  model: gpt-3.5-turbo
```

或者通过环境变量：

```bash
export AI_BASE_URL=https://api.openai.com
export AI_API_KEY=your-api-key
export AI_MODEL=gpt-3.5-turbo
```

如果不配置AI服务，系统会返回模拟数据用于测试。

### 3. 配置数据库

确保 PostgreSQL 已安装并运行，然后配置数据库连接：

```bash
# 使用环境变量（推荐）
export DB_HOST=localhost
export DB_PORT=5432
export DB_NAME=codeguardian
export DB_USERNAME=postgres
export DB_PASSWORD=your_password
```

或者修改 `src/main/resources/application.yml` 中的数据库配置。

详细设置步骤请参考 [数据库设置指南](docs/数据库设置指南.md)

### 4. 运行项目

```bash
# 编译项目
mvn clean compile

# 运行项目
mvn spring-boot:run
```

### 5. 访问应用

- 登录页面: http://localhost:8080/login
- 应用首页: http://localhost:8080
- Actuator健康检查: http://localhost:8080/actuator/health

**默认账号**: `admin` / `admin123`

## API文档

### 代码审查接口

#### 1. 审查代码片段

```bash
POST /api/review/snippet
Content-Type: application/json

{
  "codeSnippet": "public class Test { ... }",
  "language": "java",
  "taskName": "测试代码片段"
}
```

#### 2. 审查单个文件

```bash
POST /api/review/file
Content-Type: application/json

{
  "filePath": "/path/to/file.java",
  "taskName": "文件审查"
}
```

#### 3. 审查目录

```bash
POST /api/review/directory
Content-Type: application/json

{
  "directoryPath": "/path/to/directory",
  "taskName": "目录审查"
}
```

#### 4. 审查项目

```bash
POST /api/review/project
Content-Type: application/json

{
  "projectPath": "/path/to/project",
  "taskName": "项目审查"
}
```

#### 5. 获取审查任务详情

```bash
GET /api/review/task/{taskId}
```

#### 6. 获取审查发现的问题

```bash
GET /api/review/task/{taskId}/findings
```

#### 7. 查询审查历史

```bash
GET /api/review/history?name=关键词&reviewType=FILE&page=0&size=20
```

### 报告接口

#### 1. 生成报告

```bash
POST /api/report/{taskId}
```

#### 2. 获取HTML报告

```bash
GET /api/report/{taskId}/html
```

#### 3. 获取Markdown报告

```bash
GET /api/report/{taskId}/markdown
```

## 项目文档

- [系统设计文档](docs/系统设计文档.md) - 详细的系统设计说明，包括架构、数据库、API等
- [架构设计图](docs/架构设计图.md) - 系统架构图和流程图
- [数据库设计文档](docs/数据库设计文档.md) - PostgreSQL数据库详细设计文档

## 数据库初始化

数据库脚本位于 `database/` 目录：

```bash
# 1. 创建数据库
createdb -U postgres codeguardian

# 2. 执行建表脚本
psql -U postgres -d codeguardian -f database/schema.sql

# 3. （可选）插入示例数据
psql -U postgres -d codeguardian -f database/init_data.sql
```

详细说明请参考 [database/README.md](database/README.md)

## 项目结构

```
code-review-ai-agent/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/codeguardian/
│   │   │       ├── CodeReviewApplication.java    # 主启动类
│   │   │       ├── config/                       # 配置类
│   │   │       ├── constants/                    # 常量类
│   │   │       ├── controller/                   # 控制器
│   │   │       ├── dto/                          # 数据传输对象
│   │   │       ├── entity/                       # 实体类
│   │   │       ├── exception/                    # 异常处理
│   │   │       ├── repository/                  # 数据访问层
│   │   │       └── service/                      # 服务层
│   │   └── resources/
│   │       ├── application.yml                   # 主配置文件
│   │       ├── application-dev.yml               # 开发环境配置
│   │       └── application-prod.yml              # 生产环境配置
│   └── test/                                      # 测试代码
├── docs/                                          # 项目文档
│   ├── 系统设计文档.md                              # 系统设计文档
│   └── 架构设计图.md                                # 架构设计图
├── pom.xml                                        # Maven配置
└── README.md                                      # 项目说明
```

## 开发计划

- [x] 项目骨架搭建
- [x] 基础实体和DTO
- [x] 核心服务实现
- [x] REST API接口
- [x] 报告生成功能
- [x] Git集成
- [x] 异步任务处理
- [x] 规则引擎集成
- [x] RAG增强
- [x] Function Calling

## 许可证

MIT License

