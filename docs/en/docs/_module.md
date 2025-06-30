# Basic Information

|      |      |
|------|------|
| Name | weixin-java-miniapp-demo |
| Language | .java |
| Code Path | weixin-java-miniapp-demo |
| Brief Description | WeChat Mini Program backend service module, including core controllers, configuration center, and error handling system. Supports media management, session maintenance, and WeChat interaction, utilizing ThreadLocal to ensure thread safety. Features include OAuth2.0 authorization, AES decryption, file upload, and message routing, adhering to RESTful style to guarantee high-concurrency security. |

# Module List

| Name   | Type  | Description |
|-------|------|-------------|
| [_module.md](src/main/java/com/_module.md) | folder | WeChat Mini Program backend core modules, including media management, user sessions, and WeChat interaction functionalities, utilizing ThreadLocal to ensure thread safety. The configuration center manages multiple accounts and message routing, while the error handling module uniformly processes status codes such as 404/500. Dependent on WeChat SDK and Spring framework, supporting high-concurrency stateless design. |


