# Basic Information

|      |      |
|------|------|
| Name | binarywang |
| Language | .java |
| Code Path | weixin-java-miniapp-demo/src/main/java/com/github/binarywang |
| Package Name | docs.src.main.java.com.github.binarywang |
| Brief Description | WeChat Mini Program backend core modules, including media management, user sessions, and WeChat interaction functionalities, utilizing ThreadLocal to ensure thread safety. The configuration center manages multiple accounts and message routing, while the error handling module uniformly processes status codes like 404/500. Dependent on WeChat SDK and Spring framework, supporting high-concurrency stateless design. |

# Description

## Overview  
This module is a collection of backend services for WeChat Mini Programs, comprising core controllers, configuration centers, and error handling systems. Its core responsibilities include media file management, user session maintenance, interaction with WeChat servers, and unified error routing, employing ThreadLocal to ensure thread safety in a manner similar to an event bus pattern. The unified interface standards encompass POST/PGET request processing, AppID validation, JSON responses, and Spring MVC error routing. Key data structures include MediaID lists, user session information (SessionKey/OpenID), WeChat message bodies, and ErrorPage mappings. It relies on the WeChat JSSDK, AES encryption libraries, and the Spring Web framework, such as invoking WeChat APIs via JNI or dynamically loading multi-account configurations.  

## Key Business Scenarios  
The typical application pattern involves: users obtaining SessionKey after login to decrypt data, media files being relayed through MediaID, and erroneous requests automatically routed to preset pages. Business processes follow a "validate-process-cleanup" model, such as validating AppID before calling WeChat APIs for file uploads and finally clearing thread configurations. Full functionality covers OAuth2.0 authorization, AES-ECB decryption, batch multi-file uploads, and message routing (e.g., QR code processing). The interaction design resembles RESTful style, including server-side rendered interfaces (error pages) and customer service message responses, ensuring thread safety and state management under high concurrency.


### Package Internal Structure View

```mermaid
graph TD
    binarywang --> demo
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

This flowchart illustrates the directory structure of a WeChat Mini Program demo project, starting from the root directory `binarywang` and hierarchically expanding to the `miniapp` module, which includes subdirectories such as `controller`, `utils`, `error`, `config`, and their corresponding Java files. The top-level node is `binarywang`, which unfolds through three levels of directories (`demo`, `wx`, `miniapp`) and ultimately displays the specific implementation class files of each functional module.

# File List

| Name   | Type  | Description |
|-------|------|-------------|
| [demo](demo/_module.md) | package | WeChat Mini Program backend core modules, including media management, user sessions, and WeChat interaction functionalities, utilize ThreadLocal to ensure thread safety. The configuration center manages multi-account and message routing, while the error handling module uniformly processes status codes like 404/500. It relies on the WeChat SDK and Spring framework, supporting a high-concurrency stateless design. |


