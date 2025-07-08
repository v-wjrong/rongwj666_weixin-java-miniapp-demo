
# weixin-java-miniapp-demo

## Overview  
This project serves as a hub-type backend system for the WeChat Mini Program ecosystem (analogous to the "nerve center" within the WeChat ecosystem), adopting a Spring Boot monolithic architecture to implement core multi-tenant management functionalities. It primarily addresses configuration fragmentation, message routing complexity, and authentication standardization in Mini Program development, uniformly exposing WeChat ecosystem capabilities via RESTful APIs. The architectural design features a three-tier structure: the Controller layer handles WeChat protocol conversion, the Service layer integrates WeChat SDKs to implement business logic, and the Util layer encapsulates foundational capabilities such as AES encryption/decryption. Core resources include the official WeChat SDK, a multi-tenant configuration management system (e.g., `WxMaProperties.Config`), and a thread-safe session storage mechanism, effectively packaging WeChat Open Platform capabilities into an enterprise-grade development suite.  

## What is weixin-java-miniapp-demo?  
This system comprises three major modules: configuration management, message routing, and security authentication (referred to as the "three pillars" of Mini Program backends). The configuration module achieves application isolation through Zookeeper-style multi-tenant management; the message module processes 42 types of WeChat events based on the observer pattern; and the authentication module implements stateless login using the OAuth2.0 protocol. Technically, it achieves protocol adaptation via bidirectional XML-JSON conversion of WeChat message bodies and ensures data security with the AES-CBC algorithm—for instance, decrypting phone numbers requires symmetric decryption with a session_key.  

Typical use cases include managing Mini Program matrices in the education sector (unified configuration for N school subprograms), mass promotional messaging in e-commerce (uploading posters via temporary material APIs), and real-name authentication in government services (exchanging code for user phone numbers). The system uniquely features a "sandbox-production" dual-mode design, such as testing message routing chains during development by mocking WeChat servers, akin to a financial system's simulation environment.

## Quick Navigation

### 💻 Developers

- [Development Guide](summary/dev_guide.md) - Quickly get started with project development


- [Module Description](docs/_module.md) - Detailed explanation of project modules


### 🏗️ Architect

- [System Architecture](summary/system_architecture.md) - System Architecture


### ↔️ API Documentation

- [API Documentation](summary/api.md) - API Documentation

