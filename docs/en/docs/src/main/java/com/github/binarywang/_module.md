# Basic Information

|      |      |
|------|------|
| Name | binarywang |
| Language | .java |
| Code Path | weixin-java-miniapp-demo/src/main/java/com/github/binarywang |
| Package Name | docs.src.main.java.com.github.binarywang |
| Brief Description | The backend core module of the WeChat Mini Program includes media management, user information processing, and message routing functions, adhering to WeChat standards and relying on the WeChat JSSDK and Spring Boot. The error handling module uniformly manages HTTP error status codes and custom error pages. The multi-account configuration module dynamically manages Mini Program accounts and message routing. The application entry class is based on Spring Boot startup. |

# Description

## Overview  
This module serves as the core backend system for WeChat Mini Programs, integrating four major functionalities: media management, user authentication, message routing, and error handling. Built on the Spring Boot framework, it adheres to the WeChat Open Platform specifications. Key structures include Media_id lists, user session information, and message handler mappings. It relies on WeChat JSSDK, Lombok, and Spring Web components. For example, uploading media returns a media_id, user login exchanges a code for an openid, and error handling supports custom 404 pages. The JSON serialization tool employs a configurable ObjectMapper for efficient conversion.  

## Core Business Scenarios  
The system manages the entire lifecycle of Mini Programs: media files operate similarly to CDN, user authentication follows the OAuth2.0 flow, message routing adopts an event bus pattern, and error handling mimics frontend route interception. Typical workflows consist of three stages: request validation → business processing → resource cleanup. For instance, decrypting encrypted phone numbers requires session key verification. Integration cases cover five types of message processing, with exceptions handled through log-based degradation. The startup class initializes multi-account configuration services via @SpringBootApplication.


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

This flowchart illustrates the directory structure of the WeChat Mini Program Demo project, starting from the root directory binarywang and expanding hierarchically to the demo, wx, and miniapp directories. The miniapp directory contains four subdirectories: controller, utils, error, and config, along with the main program file WxMaDemoApplication.java. Each subdirectory includes specific controller classes, utility classes, error handling classes, and configuration class files, clearly reflecting the project's modular organization.

# File List

| Name   | Type  | Description |
|-------|------|-------------|
| [demo](demo/_module.md) | package | The WeChat Mini Program backend core module includes media management, user information processing, and message routing functionalities, adhering to WeChat standards and relying on WeChat JSSDK and Spring Boot. The error handling module uniformly manages HTTP error status codes and custom error pages. The multi-account configuration module dynamically manages Mini Program accounts and message routing. The application entry class is based on Spring Boot startup. |


