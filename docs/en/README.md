
# weixin-java-miniapp-demo

## Overview  
This project is a backend service solution for WeChat Mini Programs, positioned as the "server-side hub for the Mini Program ecosystem" (similar to a distributed event scheduling center). It primarily addresses service integration challenges in Mini Program development, including high-frequency requirements such as user authentication, media management, and message routing. The solution adopts a modular Spring MVC architecture, ensures thread safety through ThreadLocal, and forms a technical closed loop by leveraging the WeChat JSSDK and AES encryption libraries.  

The architecture exhibits a three-layer structure: the access layer (WeChat protocol adaptation), the business layer (session/file management), and the routing layer (error handling). Key resources include a WeChat API gateway (similar to an RPC call proxy), a dynamic configuration loader (e.g., hot updates for multi-account configurations), and a thread-safe context (secured via JNI for encryption operations). For example, when decrypting user data using AES-ECB mode, the Spring interceptor automatically validates the AppID's authenticity.  

## What is weixin-java-miniapp-demo?  
This is a collection of backend functionalities for WeChat Mini Programs, comprising four core interaction modules: the authentication module (similar to an OAuth2.0 gateway), the media center (similar to a CDN relay station), the message bus (similar to an event dispatcher), and the error router (similar to a traffic flow valve). The technical implementation is based on WeChat's open protocols, such as using SessionKey for user state isolation and converting temporary WeChat files via MediaID.  

Typical use cases include e-commerce Mini Programs: user login triggers an AES decryption chain (similar to an SSL handshake), product image uploads are stored as MediaIDs (similar to object storage keys), and payment messages are pushed through customer service APIs (similar to MQ message queues). In specific implementations, QR code processing follows a three-phase model of "validation-generation-cleanup," while error pages are dynamically rendered via Spring MVC's ViewResolver, akin to server-side SSR technology.

## Quick Navigation

### Developers
- [Development Guide](summary/dev_guide.md) - Quickly get started with project development
- [Module Description](docs/_module.md) - Detailed explanation of project modules
### Architect
- [System Architecture](summary/system_architecture.md) - System Architecture
### API Documentation
- [API Documentation](summary/api.md) - API Documentation