
# weixin-java-miniapp-demo

## Overview  
This project is a lightweight backend solution for the WeChat Mini Program ecosystem, with its core positioning as a "Mini Program Business Capability Middle Platform," akin to an adaptation layer connecting WeChat's native capabilities with enterprise applications. It primarily addresses the standardization of server-side issues in rapid mobile development by encapsulating WeChat protocols to achieve unified access to core functionalities such as identity, messaging, and file handling. Built on a Spring Boot monolithic architecture, it features built-in multi-tenant isolation mechanisms, with key resources including a RESTful SDK (for interfacing with WeChat APIs) and an AES encryption/decryption toolchain.  

The architectural characteristics emphasize protocol adaptation and business decoupling. For instance, it abstracts file storage details via Media_id, resembling a distributed file proxy, while the session module employs a dual-token verification mechanism, analogous to an OAuth2.0 authorization relay. Core technology selections encompass WeChat's custom communication protocol, Spring Web MVC routing, and Lombok annotation programming, with typical implementations such as multi-node configuration synchronization via Zookeeper.  

## What is weixin-java-miniapp-demo?  
This component is a modular implementation of WeChat Mini Program backend capabilities, comprising four functional modules: Media Gateway, Authentication Center, Message Bus, and Exception Circuit Breaker. The Media Gateway implements file hosting based on HTTP chunked upload protocols, resembling a simplified CDN edge node. The Authentication Center performs chained identity verification via the Code2Session interface, with a technical principle similar to JWT token relay. Modules collaborate through the Spring IOC container—for example, the message handler relies on the AES-CBC decryption library to process WeChat-encrypted data packets.  

Typical application scenarios include user profile construction in e-commerce (phone number decryption) and courseware distribution in education (temporary media management). Specific implementation examples include using Redis to cache SessionKeys for improved authentication efficiency and uniformly packaging WeChat error codes via a global exception interceptor. Its multi-account management system can be likened to the Sidecar pattern in service mesh, where each tenant independently loads configuration instances to ensure physical isolation for enterprise multi-Mini Program accounts.

## Quick Navigation

### 💻 Developers

- [Development Guide](summary/dev_guide.md) - Quickly get started with project development


- [Module Description](docs/_module.md) - Detailed explanation of project modules


### 🏗️ Architect

- [System Architecture](summary/system_architecture.md) - System Architecture


### ↔️ API Documentation

- [API Documentation](summary/api.md) - API Documentation

