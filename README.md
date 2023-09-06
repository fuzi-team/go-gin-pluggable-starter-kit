# Fuzi 框架

Fuzi 是一个基于 Gin 构建的高度模块化和可插拔的 Go 应用框架。

## 目录
1. [安装](#安装)
2. [快速开始](#快速开始)
3. [特点](#特点)
    - [模块](#模块)
    - [中间件](#中间件)
    - [插件](#插件)
4. [使用方法](#使用方法)
5. [贡献](#贡献)
6. [许可证](#许可证)

## 安装

```bash
go get -u github.com/你的用户名/fuzi
```

## 快速开始

```go
package main

import (
    "fuzi/pkg/app"
    "myproject/modules/user"
    "myproject/middlewares/auth"
)

func main() {
    myApp := app.New()
    myApp.UseModule(&user.UserModule{})
    myApp.UseMiddleware(&auth.AuthMiddleware{})
    myApp.Initialize()
    myApp.Run(":8080")
}
```

## 特点

### 模块

模块是 Fuzi 的一个核心构造，负责对特定功能或者功能组进行封装。模块可以包括路由定义、依赖注入提供者、服务等。

- **独立性**：模块可以作为独立单位进行测试。
- **可组合**：可以将多个模块组合成一个更大的应用。

#### 示例

```go
type UserModule struct{}

func (m *UserModule) Initialize() error {
    // 初始化逻辑
}

func (m *UserModule) RegisterRoutes(engine *gin.Engine) {
    // 注册路由
}
```

### 中间件

中间件允许你在处理 HTTP 请求的生命周期中插入自定义逻辑。这可以用于权限检查、日志、缓存等。

- **可重用**：一次编写，多次使用。
- **灵活性**：可以按照需要在多个地方应用相同的中间件。

#### 示例

```go
type AuthMiddleware struct{}

func (m *AuthMiddleware) Apply(engine *gin.Engine) {
    // 应用中间件逻辑
}
```

### 插件

插件提供了一种用于添加特定功能的可扩展机制。例如，一个插件可以添加数据库支持、身份验证系统或者其他自定义功能。

- **可插拔**：可以轻松地添加或删除不影响整个系统。
- **可配置**：根据需要定制插件的行为。

#### 示例

```go
type AuthPlugin struct{}

func (p *AuthPlugin) Initialize() error {
    // 初始化逻辑
}

func (p *AuthPlugin) RegisterRoutes(engine *gin.Engine) {
    // 注册路由
}
```

## 使用方法

有关详细的使用方法，请查看 [Wiki](https://github.com/你的用户名/fuzi/wiki)。

## 贡献

欢迎提出问题和拉取请求。

## 许可证

MIT 许可证
