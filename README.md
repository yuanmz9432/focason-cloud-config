# Focason Cloud Config

本项目是 `focason-cloud-starter` 中 config 模块对应的配置仓库，用于集中管理各个微服务模块的环境配置文件。

## 📋 项目说明

本仓库存储了 Focason Cloud 项目中各服务模块的配置文件，采用 Spring Cloud Config 的配置管理模式，便于集中管理和动态更新各服务的配置信息。

## 📁 目录结构

```
focason-cloud-config/
├── focason-gateway.yml              # Gateway 网关服务配置
├── focason-platform-service.yml     # Platform 平台服务配置
└── README.md                        # 项目说明文档
```

## 🔧 配置文件说明

### focason-gateway.yml

Gateway 网关服务的配置文件，包含：
- **日志配置**：日志文件路径和日志级别设置

### focason-platform-service.yml

Platform 平台服务的配置文件，包含：
- **日志配置**：日志文件路径和日志级别设置
- **邮件配置**：发送者名称和邮箱地址
- **AWS 配置**：
  - AWS 区域设置
  - S3 存储桶配置
  - 预签名 URL 有效期设置

## 🚀 使用方法

### 环境变量

配置文件中支持通过环境变量进行覆盖，常用环境变量包括：

- `LOG_LEVEL`: 日志级别（默认：INFO）
- `EMAIL_SEND_BY`: 邮件发送者名称（默认：Focason Lab Team）
- `EMAIL_SEND_FROM`: 邮件发送者地址（默认：noreply@focason.com）
- `AWS_REGION`: AWS 区域（默认：ap-northeast-1）
- `AWS_BUCKET_NAME`: S3 存储桶名称（默认：focason-cloud-file）
- `PRESIGNED_URL_VALID_MINUTES`: 预签名 URL 有效期（分钟，默认：1440）

### 配置服务对接

确保 Spring Cloud Config Server 已正确配置并能够访问本仓库，各服务模块可通过以下方式引用配置：

```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: <本仓库地址>
          search-paths: '{application}'
```

## 📝 配置说明

### 日志配置

所有服务都包含统一的日志配置：
- 日志文件存储在 `logs/` 目录下
- 日志级别可通过环境变量 `LOG_LEVEL` 动态调整

### 邮件配置

Platform 服务支持邮件发送功能，可通过环境变量自定义：
- 发送者显示名称
- 发送者邮箱地址

### AWS 配置

Platform 服务集成了 AWS S3 存储功能：
- 支持自定义 AWS 区域
- 支持配置 S3 存储桶名称
- 支持设置预签名 URL 有效期（最大 10080 分钟）

## 🔄 更新流程

1. 在本仓库中修改对应的配置文件
2. 提交并推送到远程仓库
3. 各服务模块通过 Spring Cloud Config 自动拉取最新配置
4. 如需立即生效，可触发服务的配置刷新端点

## ⚠️ 注意事项

- 生产环境敏感信息（如密码、密钥）应使用环境变量或密钥管理服务，不要直接写入配置文件
- 修改配置后请确保测试环境的验证通过
- 配置文件格式需符合 YAML 规范，注意缩进和语法

## 📞 联系方式

如有问题或建议，请联系 Focason Lab Team。

