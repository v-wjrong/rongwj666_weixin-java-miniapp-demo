# Basic Information

|      |      |
|------|------|
| Name | demo |
| Language | .java |
| Code Path | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo |
| Package Name | docs.src.main.java.com.github.binarywang.demo |
| Brief Description | The Spring Boot WeChat Mini Program Demo includes a startup class, error handling, JSON utilities, controllers, and configuration modules. The startup class follows a standard structure, the error module handles 404/500 redirects, the utility class provides JSON serialization, the controllers manage media and user messages, and the configuration module handles multi-account initialization. |

# Description

## Overview  
This module is a collection of backend services for WeChat Mini Programs, with core responsibilities including application startup configuration, error handling, business logic control, and multi-tenant management. Built using the Spring Boot framework, it follows the standard MVC pattern and exposes RESTful interfaces and WeChat callback interfaces through Controllers. Key data structures cover error page mappings (ErrorPage), user session information (sessionKey/openid), and WeChat message objects. External dependencies include Spring Web, the WeChat Mini Program Java SDK, and JSON processing tools. For example, WxMaDemoApplication serves as the startup entry, JsonUtils handles serialization, and WxMaProperties manages multi-account configurations.  

## Core Business Scenarios  
The module implements a complete backend workflow for WeChat Mini Programs, resembling a SaaS service architecture. Primary business flows include: 1) An error interception chain handling status codes like 404/500; 2) Media management for temporary file uploads and downloads; 3) User services for login authorization and sensitive data decryption; 4) A configuration center for initializing multi-tenant instances. Typical interactions, such as user login → media operations → message processing, ensure thread safety via ThreadLocal. API integration examples can be seen in the error handling subsystem, multi-format message routing (XML/JSON), and unified exception capture for WeChat APIs.


### Package Internal Structure View

```mermaid
graph TD
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
```

This flowchart illustrates the core structure of the WeChat Mini Program Demo project. Starting from the root directory 'demo', it expands into 'wx' and 'miniapp' levels. The 'miniapp' directory includes the main application class, error handling module, utility classes, controllers, and configuration modules. Each submodule is further divided into specific implementation classes, such as controllers containing media, user, and portal controllers, while the configuration module comprises property and configuration classes.

# File List

| Name   | Type  | Description |
|-------|------|-------------|
| [wx](wx/_module.md) | package | The Spring Boot WeChat Mini Program Demo includes a startup class, error handling, JSON utilities, controllers, and configuration modules. The startup class follows a standard structure, the error module handles 404/500 redirects, the utility class provides JSON serialization, the controllers manage media and user messages, and the configuration module handles multi-account initialization. |


