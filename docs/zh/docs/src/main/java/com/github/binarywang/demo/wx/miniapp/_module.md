# 基础信息

|      |      |
|------|------|
| 名称 | miniapp |
| 编码语言 | .java |
| 代码路径 | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo/wx/miniapp |
| 包名 | docs.src.main.java.com.github.binarywang.demo.wx.miniapp |
| 概述说明 | Spring Boot微信小程序Demo入口类，含错误处理、JSON工具、控制器和配置模块。错误处理含404/500跳转，JSON工具序列化对象，控制器管理媒体、用户和消息，配置模块管理账号和路由。 |

# 说明

## 概述  
该模块是微信小程序后端服务的核心系统，采用Spring Boot框架实现，主要职责包括小程序账号配置管理、微信消息路由处理、用户会话维护及错误统一处理。系统遵循RESTful接口规范，通过Controller暴露媒体管理、用户认证等API，并集成JSON序列化工具。关键数据结构涵盖微信消息体、用户会话信息和错误状态码映射。外部依赖包括Spring Web、微信SDK、AES加密库和Lombok。例如通过`WxMaProperties.Config`管理多租户配置，或使用`ErrorController`渲染统一错误页。

## 主要业务场景  
模块支持四类典型场景：1)多账号配置初始化（类似微服务配置中心），2)媒体文件传输（如临时素材上传），3)用户OAuth式登录（校验code获取openid），4)微信消息处理（类似事件总线路由）。业务流程均采用"校验-处理-清理"模式，例如用户登录需验证appid并清理ThreadLocal数据。交互方式包含同步HTTP请求（如GET获取二维码）和消息回调（如处理加密推送）。典型应用案例包括群发消息配置、手机号解密及404错误兜底页展示。


### 包内部结构视图

```mermaid
graph TD
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

该流程图展示了微信小程序Demo项目的核心结构，包含主应用类、错误处理模块、工具类、控制器和配置模块。顶层节点为miniapp目录，下分5个子模块，其中error模块包含2个错误处理类，utils模块含1个工具类，controller模块含3个控制器类，config模块含3个配置类，整体呈现清晰的层级关系。

# 文件列表

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [WxMaDemoApplication.java](WxMaDemoApplication.md) | file | SpringBoot应用启动类，包含主方法运行Spring应用。 |
| [error](error/_module.md) | package | Spring MVC控制器处理404/500错误，返回error视图。配置类注册错误页面，404跳/error/404，500跳/error/500。 |
| [utils](utils/_module.md) | package | JsonUtils工具类使用ObjectMapper实现对象转JSON字符串，自动忽略null值并格式化输出，异常时返回null。 |
| [controller](controller/_module.md) | package | 微信小程序控制器类：媒体控制器处理文件上传下载，用户控制器管理登录/信息/手机号功能，门户控制器负责认证和消息处理。所有接口验证appid并确保线程安全。 |
| [config](config/_module.md) | package | 微信小程序Java配置类：WxMaProperties定义小程序核心配置项；WxMaConfiguration初始化多账号服务及消息路由；ResourcesConfig配置本地文件存储和跨域访问。 |


