# 基础信息

|      |      |
|------|------|
| 名称 | miniapp |
| 编码语言 | .java |
| 代码路径 | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo/wx/miniapp |
| 包名 | docs.src.main.java.com.github.binarywang.demo.wx.miniapp |
| 概述说明 | Spring Boot微信小程序Demo，含启动类、控制器、JSON工具、错误处理和配置模块。控制器处理媒体、用户和消息，工具类处理JSON序列化，错误模块统一处理HTTP错误，配置模块管理多账号和消息服务。 |

# 说明

## 概述  
该模块是微信小程序后端服务的Spring Boot实现，核心职责包括媒体文件管理、用户会话处理、微信消息交互和错误统一处理。采用RESTful接口规范，支持JSON/XML数据格式，关键数据结构涵盖Media_id列表、用户会话信息（sessionKey/openid）和微信消息体。外部依赖微信服务器API、AES加密库、Spring Web框架和Lombok。例如媒体控制器处理文件上传，用户控制器管理登录授权，配置模块初始化多账号服务。

## 主要业务场景  
模块支持四类典型交互：媒体传输（类似FTP）、身份认证（类似OAuth）、消息处理（类似事件总线）和错误兜底（类似路由拦截器）。业务流程遵循"校验-处理-清理"模式，例如用户登录先验证code再获取会话信息。典型应用包括上传临时素材、解密用户手机号和处理加密消息，所有接口严格校验appid确保多租户隔离。集成案例可见订阅消息推送和500错误页渲染。


### 包内部结构视图

```mermaid
graph TD
    miniapp --> WxMaDemoApplication.java
    miniapp --> controller
    miniapp --> utils
    miniapp --> error
    miniapp --> config
    controller --> WxMaMediaController.java
    controller --> WxMaUserController.java
    controller --> WxPortalController.java
    utils --> JsonUtils.java
    error --> ErrorController.java
    error --> ErrorPageConfiguration.java
    config --> WxMaProperties.java
    config --> WxMaConfiguration.java
```

该流程图展示了微信小程序Demo项目的核心代码结构，根节点miniapp下包含主应用类、控制器包、工具类包、错误处理包和配置包。控制器包中包含三个功能控制器，分别处理媒体、用户和门户请求；错误处理包包含错误控制器和页面配置；配置包则存放小程序属性及配置类。整体结构清晰体现了典型Spring Boot应用的分层架构。

# 文件列表

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [WxMaDemoApplication.java](WxMaDemoApplication.md) | file | SpringBoot应用启动类，包含主方法运行Spring应用。 |
| [config](config/_module.md) | package | WxMaProperties类配置微信小程序属性，含appid、secret等字段。WxMaConfiguration类初始化小程序服务和消息路由，定义各类消息处理器逻辑。 |
| [error](error/_module.md) | package | Spring MVC控制器处理404/500错误，返回error视图。配置类注册错误页面，404跳/error/404，500跳/error/500。 |
| [utils](utils/_module.md) | package | JsonUtils工具类使用ObjectMapper实现对象转JSON字符串，自动忽略null值并格式化输出，异常时返回null。 |
| [controller](controller/_module.md) | package | 微信小程序控制器类：媒体控制器处理文件上传下载，用户控制器管理登录/信息/手机号功能，门户控制器负责认证和消息处理。所有接口验证appid并确保线程安全。 |


