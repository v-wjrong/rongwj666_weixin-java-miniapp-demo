# Basic Information

|      |      |
|------|------|
| Name | demo |
| Language | .java |
| Code Path | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo |
| Package Name | docs.src.main.java.com.github.binarywang.demo |
| Brief Description | Spring Boot WeChat Mini Program Demo entry class, including error handling, JSON utilities, controllers, and configuration modules. Error handling covers 404/500 redirects, JSON utilities serialize objects, controllers manage media, users, and messages, while configuration modules handle account and routing settings. |

# Description

## Overview  
This module serves as the core system for the WeChat Mini Program backend, implemented using the Spring Boot framework. Its primary responsibilities include Mini Program account configuration management, WeChat message routing, user session maintenance, and unified error handling. The system adheres to RESTful API standards, exposing APIs for media management, user authentication, and more through Controllers, with integrated JSON serialization tools. Key data structures encompass WeChat message bodies, user session information, and error status code mappings. External dependencies include Spring Web, WeChat SDK, AES encryption libraries, and Lombok. For example, multi-tenant configurations are managed via `WxMaProperties.Config`, while `ErrorController` renders unified error pages.  

## Key Business Scenarios  
The module supports four typical scenarios: 1) Multi-account configuration initialization (similar to a microservice configuration center), 2) Media file transfer (e.g., temporary material uploads), 3) User OAuth-style login (validating code to obtain openid), and 4) WeChat message processing (similar to event bus routing). Business processes follow a "validate-process-cleanup" pattern—for instance, user login requires appid verification and ThreadLocal data cleanup. Interaction methods include synchronous HTTP requests (e.g., GET for QR codes) and message callbacks (e.g., handling encrypted push notifications). Typical use cases include bulk message configuration, phone number decryption, and 404 error fallback page display.


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
    config --> ResourcesConfig.java
```

This flowchart illustrates the core directory structure of a WeChat Mini Program demo project, starting from the root directory 'demo' and expanding hierarchically to 'wx' and 'miniapp' directories. The 'miniapp' directory includes the main application file, error handling module, utility classes, controllers, and configuration modules. Each module contains specific implementation files such as error controllers, JSON utility classes, media controllers, and property configurations, forming a clear hierarchical relationship.

# File List

| Name   | Type  | Description |
|-------|------|-------------|
| [wx](wx/_module.md) | package | Spring Boot WeChat Mini Program Demo entry class, including error handling, JSON utilities, controllers, and configuration modules. Error handling covers 404/500 redirection, JSON utilities serialize objects, controllers manage media, users, and messages, while the configuration module handles account and routing settings. |


