
# weixin-java-miniapp-demo

## Overview  
This project serves as the backend core system for WeChat Mini Programs (analogous to the "central processing unit" of a mini-program engine), positioned as a full-featured service hub within the WeChat ecosystem. It primarily addresses four core challenges in mini-program development: media resource hosting, security authentication, message distribution, and system fault tolerance. Built on a Spring Boot monolithic architecture, it encapsulates WeChat JSSDK capabilities into standardized service interfaces through modular design. Key resources include an auto-configured ObjectMapper serialization tool and a prebuilt multi-account management module.  

The system architecture follows a "funnel-shaped" processing flow: the top layer interfaces with WeChat Open Platform specifications, the middle layer simplifies business logic via Lombok, and the底层 relies on Spring Web for HTTP communication. Distinctive features include temporary media management through Media_id lists (similar to short-lifecycle CDN storage), an OAuth2.0-based code-openid conversion mechanism, and hierarchical error handling modeled after frontend route interception. For instance, in user login scenarios, the system sequentially completes the full chain of WeChat credential verification → session key generation → distributed session storage.  

## What is weixin-java-miniapp-demo?  
This system is a Java implementation reference framework for WeChat Mini Program backend functionalities (akin to a Lego base module set), comprising four core modules: media management, user authentication, message routing, and error handling. Modules interact via an event bus pattern: the authentication module outputs user credentials, the media module consumes upload events, message processors map types to respective business logic, and exceptions are ultimately degraded uniformly by a global interceptor. Technically, it leverages WeChat JSSDK as the protocol foundation, such as implementing two-way authentication equivalent to banking U盾 through the code2session interface.  

Typical application scenarios exhibit a "sandwich" structure: frontend requests first pass through a signature verification layer (similar to customs security checks), the business layer automatically injects WeChat context (e.g., retrieving user info via @WxSession annotation), and standardized responses are output via a configurable ObjectMapper. Specific use cases include encrypted phone number decryption (requiring session keys as decoders) and automatic seven-day cleanup of temporary media (analogous to supermarket clearance mechanisms). The system uniquely incorporates a multi-account configuration service, enabling a single instance to manage multiple mini-program accounts simultaneously—comparable to a hotel front desk's multi-keycard management system.

## Quick Navigation

### 💻 Developers

- [Development Guide](summary/dev_guide.md) - Quickly get started with project development


- [Module Description](docs/_module.md) - Detailed explanation of project modules


### 🏗️ Architect

- [System Architecture](summary/system_architecture.md) - System Architecture


### ↔️ API Documentation

- [API Documentation](summary/api.md) - API Documentation

