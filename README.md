
# weixin-java-miniapp-demo

## 概述  
该工程是微信小程序后端服务解决方案，定位为"小程序生态系统的服务端中枢"（类似分布式事件调度中心）。核心解决小程序开发中的服务集成问题，包括用户认证、媒体管理、消息路由等高频需求。采用模块化Spring MVC架构，通过ThreadLocal实现线程安全，依赖微信JSSDK和AES加密库形成技术闭环。  

架构呈现三层特征：接入层（微信协议适配）、业务层（会话/文件管理）、路由层（错误处理）。关键资源包含微信API网关（类似RPC调用代理）、动态配置加载器（如多账号配置热更新）和线程安全上下文（通过JNI保障加密操作）。例如使用AES-ECB模式解密用户数据时，通过Spring拦截器自动校验AppID有效性。  

## 什么是weixin-java-miniapp-demo?  
这是微信小程序后端功能集合，包含四大交互模块：认证模块（类似OAuth2.0网关）、媒体中心（类似CDN中转站）、消息总线（类似事件分发器）、错误路由器（类似流量导流阀）。技术实现基于微信开放协议，例如用SessionKey实现用户态隔离，通过MediaID转换微信临时文件。  

典型应用场景如电商小程序：用户登录时触发AES解密链（类似SSL握手），商品图片上传转为MediaID存储（类似对象存储Key），支付消息通过客服接口推送（类似MQ消息队列）。具体实现中，二维码处理采用"校验-生成-清理"三阶段模型，错误页面通过Spring MVC的ViewResolver动态渲染，类似服务端SSR技术。

## 快速导航

### 开发者
- [开发指南](docs/zh/summary/dev_guide.md) - 快速上手项目开发
- [模块说明](docs/zh/docs/_module.md) - 项目模块详细说明
### 架构师
- [系统架构](docs/zh/summary/system_architecture.md) - 系统架构
### API 文档
- [API 文档](summary/api.md) - API 文档