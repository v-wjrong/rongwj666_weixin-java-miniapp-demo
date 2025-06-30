# 基础信息

|      |      |
|------|------|
| 名称 | miniapp |
| 编码语言 | .java |
| 代码路径 | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo/wx/miniapp |
| 包名 | docs.src.main.java.com.github.binarywang.demo.wx.miniapp |
| 概述说明 | 微信小程序后端核心模块，含媒体管理、用户会话和微信交互功能，采用ThreadLocal确保线程安全。配置中心管理多账号和消息路由，错误处理模块统一处理404/500等状态码。依赖微信SDK和Spring框架，支持高并发无状态设计。 |

# 说明

## 概述  
该模块是微信小程序后端服务集合，包含核心控制器、配置中心和错误处理系统。核心职责包括媒体文件管理、用户会话维护、微信服务器交互及统一错误路由，采用ThreadLocal保证线程安全，类似事件总线模式。统一接口规范涵盖POST/PGET请求处理、AppID校验、JSON响应及Spring MVC错误路由。关键数据结构包含MediaID列表、用户会话信息（SessionKey/OpenID）、微信消息体和ErrorPage映射。依赖微信JSSDK、AES加密库及Spring Web框架，例如通过JNI调用微信API或动态加载多账号配置。

## 主要业务场景  
典型应用模式为：用户登录获取SessionKey后解密数据，媒体文件通过MediaID中转，错误请求自动路由至预设页面。业务流程均遵循"校验-处理-清理"模式，例如上传文件时校验AppID后调用微信API，最后清除线程配置。完整功能覆盖OAuth2.0授权、AES-ECB解密、多文件批量上传及消息路由（如二维码处理）。交互设计类似RESTful风格，包含服务端渲染接口（错误页）和客服消息响应，确保高并发下的线程安全与状态管理。


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

该流程图展示了微信小程序Demo项目的核心结构，根节点miniapp下包含5个子模块：主应用类、控制器包、工具类包、错误处理包和配置包。控制器包中包含3个不同功能的控制器类，错误处理包和配置包各包含2个相关类，工具类包包含1个JSON工具类。整体结构清晰体现了典型Spring Boot应用的分层架构。

# 文件列表

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [WxMaDemoApplication.java](WxMaDemoApplication.md) | file | SpringBoot应用启动类，包含主方法运行Spring应用。 |
| [config](config/_module.md) | package | WxMaProperties类配置微信小程序属性，含appid、secret等字段。WxMaConfiguration类初始化小程序服务，设置消息路由规则，处理文本、图片等消息。 |
| [error](error/_module.md) | package | Spring MVC控制器ErrorController处理/error路径，包含404和500错误处理方法返回error视图。ErrorPageConfiguration类配置404和500错误页面跳转路径。 |
| [utils](utils/_module.md) | package | JsonUtils工具类，使用ObjectMapper配置非NULL字段序列化和格式化输出，提供toJson方法将对象转为JSON字符串，异常时返回null。 |
| [controller](controller/_module.md) | package | 微信小程序三个控制器类：媒体管理类处理文件上传下载；用户管理类提供登录、用户信息和手机号接口；后台类处理微信认证和消息推送。均清理ThreadLocal配置，记录日志并处理异常。 |


