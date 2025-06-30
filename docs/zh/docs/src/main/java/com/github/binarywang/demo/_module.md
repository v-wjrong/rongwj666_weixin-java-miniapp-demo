# 基础信息

|      |      |
|------|------|
| 名称 | demo |
| 编码语言 | .java |
| 代码路径 | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo |
| 包名 | docs.src.main.java.com.github.binarywang.demo |
| 概述说明 | 微信小程序后端核心模块，包含媒体管理、用户会话和微信交互功能，依赖微信SDK和Lombok。支持文件上传、身份认证和消息路由，流程包括校验、处理和清理。错误处理模块统一管理404/500响应。配置模块管理小程序属性和消息服务初始化。Spring Boot应用入口类启动整个Demo。 |

# 说明

## 概述  
该模块是微信小程序后端服务的集成解决方案，核心职责包括媒体文件管理、用户会话管理、微信服务器交互和统一错误处理。接口规范要求验证AppID有效性，遵循Spring MVC标准，并通过`wx.miniapp`前缀注入配置。关键数据结构涵盖media_id、用户会话对象、微信消息封装体和WxMaProperties.Config配置类。外部依赖微信SDK、Spring框架和Lombok工具库。例如媒体控制器处理多文件上传，错误控制器返回统一视图，配置类实现多账号管理。

## 主要业务场景  
模块支持四类典型交互：媒体文件传输（类似网盘接口）、用户认证（类似OAuth2.0）、微信消息路由（类似事件总线模式）和HTTP错误处理（类似Web服务器错误页）。完整业务流程包含凭证校验→业务处理→资源清理三阶段，例如用户登录验证code或异常时重定向错误页。集成案例覆盖文件上传、会话解密、消息响应和错误提示，如POST接口处理加密消息或GET返回404视图。所有交互通过标准Spring MVC控制器实现。


### 包内部结构视图

```mermaid
graph TD
    demo --> wx
    wx --> miniapp
    miniapp --> controller
    miniapp --> utils
    miniapp --> error
    miniapp --> config
    miniapp --> WxMaDemoApplication.java
    controller --> WxMaMediaController.java
    controller --> WxMaUserController.java
    controller --> WxPortalController.java
    utils --> JsonUtils.java
    error --> ErrorController.java
    error --> ErrorPageConfiguration.java
    config --> WxMaProperties.java
    config --> WxMaConfiguration.java
```

该流程图展示了微信小程序Demo项目的核心结构，从根目录demo开始，逐级展开到wx和miniapp目录。miniapp下包含控制器、工具类、错误处理、配置等子模块，每个模块又包含具体的实现类文件。整个结构清晰地反映了微信小程序后端代码的组织方式，控制器处理不同业务请求，工具类提供辅助功能，错误处理模块管理异常情况，配置模块负责参数设置。

# 文件列表

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [wx](wx/_module.md) | package | 微信小程序后端核心模块，包含媒体管理、用户会话和微信交互功能，依赖微信SDK和Lombok。支持文件上传、身份认证和消息路由，流程包括校验、处理和清理。错误处理模块统一管理404/500响应。配置模块管理小程序属性和消息服务初始化。Spring Boot应用入口类启动整个Demo。 |


