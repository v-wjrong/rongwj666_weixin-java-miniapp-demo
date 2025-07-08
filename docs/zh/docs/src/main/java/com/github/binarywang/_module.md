# 基础信息

|      |      |
|------|------|
| 名称 | binarywang |
| 编码语言 | .java |
| 代码路径 | weixin-java-miniapp-demo/src/main/java/com/github/binarywang |
| 包名 | docs.src.main.java.com.github.binarywang |
| 概述说明 | Spring Boot微信小程序Demo入口类，含错误处理、JSON工具、控制器和配置模块。错误处理含404/500跳转，JSON工具序列化对象，控制器管理媒体、用户和消息，配置模块管理账号和路由。 |

# 说明

## 概述  
该模块是微信小程序后端服务的核心系统，采用Spring Boot框架实现，主要职责包括小程序账号配置管理、微信消息路由处理、用户会话维护及错误统一处理。系统遵循RESTful接口规范，通过Controller暴露媒体管理、用户认证等API，并集成JSON序列化工具。关键数据结构涵盖微信消息体、用户会话信息和错误状态码映射。外部依赖包括Spring Web、微信SDK、AES加密库和Lombok。例如通过`WxMaProperties.Config`管理多租户配置，或使用`ErrorController`渲染统一错误页。

## 主要业务场景  
模块支持四类典型场景：1)多账号配置初始化（类似微服务配置中心），2)媒体文件传输（如临时素材上传），3)用户OAuth式登录（校验code获取openid），4)微信消息处理（类似事件总线路由）。业务流程均采用"校验-处理-清理"模式，例如用户登录需验证appid并清理ThreadLocal数据。交互方式包含同步HTTP请求（如GET获取二维码）和消息回调（如处理加密推送）。典型应用案例包括群发消息配置、手机号解密及404错误兜底页展示。


### 包内部结构视图

```mermaid
graph TD
    binarywang --> demo
    demo --> wx
    wx --> miniapp
    miniapp --> WxMaDemoApplication.java
    miniapp --> error
    miniapp --> utils
    miniapp --> controller
    miniapp --> config
    error --> ErrorController.java
    error --> ErrorPageConfiguration.java
    utils --> JsonUtils.java
    controller --> WxMaMediaController.java
    controller --> WxMaUserController.java
    controller --> WxPortalController.java
    config --> WxMaProperties.java
    config --> WxMaConfiguration.java
    config --> ResourcesConfig.java
```

该流程图展示了微信小程序Demo项目的核心代码结构，从根目录binarywang开始，逐级展开到demo、wx和miniapp层级。miniapp作为主模块包含启动类WxMaDemoApplication.java，并分支出error（错误处理）、utils（工具类）、controller（控制器）和config（配置）四个子模块。每个子模块下包含对应的功能类文件，如错误处理模块包含错误控制器和页面配置，配置模块包含属性配置和资源配置等。整体结构清晰体现了典型Spring Boot应用的分层架构。

# 文件列表

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [demo](demo/_module.md) | package | Spring Boot微信小程序Demo入口类，含错误处理、JSON工具、控制器和配置模块。错误处理含404/500跳转，JSON工具序列化对象，控制器管理媒体、用户和消息，配置模块管理账号和路由。 |


