# Basic Information

|      |      |
|------|------|
| Name | demo |
| Language | .java |
| Code Path | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo |
| Package Name | docs.src.main.java.com.github.binarywang.demo |
| Brief Description | WeChat Mini Program backend core modules, including media management, user sessions, and WeChat interaction functionalities, utilize ThreadLocal to ensure thread safety. The configuration center manages multi-account and message routing, while the error handling module uniformly processes status codes like 404/500. It relies on the WeChat SDK and Spring framework, supporting a high-concurrency stateless design. |

# Description

## Overview  
This module is a collection of backend services for WeChat Mini Programs, comprising core controllers, configuration centers, and error handling systems. Its core responsibilities include media file management, user session maintenance, interaction with WeChat servers, and unified error routing, employing ThreadLocal to ensure thread safety in a pattern similar to an event bus. The unified interface specification covers POST/PGET request handling, AppID validation, JSON responses, and Spring MVC error routing. Key data structures include MediaID lists, user session information (SessionKey/OpenID), WeChat message bodies, and ErrorPage mappings. It relies on the WeChat JSSDK, AES encryption libraries, and the Spring Web framework, such as invoking WeChat APIs via JNI or dynamically loading multi-account configurations.  

## Primary Business Scenarios  
The typical application pattern involves: users obtaining a SessionKey after login to decrypt data, media files being transferred via MediaID, and erroneous requests automatically routed to preset pages. Business processes follow a "validate-process-cleanup" model, such as validating the AppID before calling WeChat APIs for file uploads and finally clearing thread configurations. Full functionality covers OAuth2.0 authorization, AES-ECB decryption, batch multi-file uploads, and message routing (e.g., QR code processing). The interaction design follows a RESTful style, including server-side rendered interfaces (error pages) and customer service message responses, ensuring thread safety and state management under high concurrency.


### Package Internal Structure View

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

This flowchart illustrates the core structure of the WeChat Mini Program Demo project, starting from the root directory `demo` and hierarchically expanding to the `wx/miniapp` submodule. It includes key directories such as `controller`, `utils`, `error`, and `config`, along with their corresponding Java class files. The `controller` directory contains three controller classes, while the `error` and `config` directories each have two configuration classes. The `utils` directory includes one utility class, and the outermost layer is the main application class `WxMaDemoApplication.java`.

# File List

| Name   | Type  | Description |
|-------|------|-------------|
| [wx](wx/_module.md) | package | WeChat Mini Program backend core modules, including media management, user sessions, and WeChat interaction functionalities, utilize ThreadLocal to ensure thread safety. The configuration center manages multi-account and message routing, while the error handling module uniformly processes status codes like 404/500. It relies on the WeChat SDK and Spring framework, supporting a high-concurrency stateless design. |


