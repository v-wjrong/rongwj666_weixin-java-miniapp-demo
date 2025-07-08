# Basic Information

|      |      |
|------|------|
| Name | WxMaProperties |
| Language | .java |
| Code Path | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo/wx/miniapp/config/WxMaProperties.java |
| Package Name | com.github.binarywang.demo.wx.miniapp.config |
| Dependencies | ['java.util.List', 'org.springframework.boot.context.properties.ConfigurationProperties', 'lombok.Data'] |
| Brief Description | This is a WeChat Mini Program configuration class, which includes multiple Mini Program configuration items. Each configuration item has fields such as appid, secret, token, aesKey, and message format msgDataFormat. |

# Description

This is a Java class used for configuring WeChat Mini Program related properties. The main class WxMaProperties uses the @ConfigurationProperties annotation with the prefix wx.miniapp and contains a list of Config type named configs. The Config class defines the core configuration items for the WeChat Mini Program: appid (Mini Program ID), secret (Mini Program secret key), token (message server token), aesKey (message encryption key), and msgDataFormat (message format, supporting XML or JSON). All fields automatically generate getter and setter methods through Lombok's @Data annotation.

# Class Summary

| Name   | Type  | Description |
|-------|------|-------------|
| WxMaProperties | class | The WxMaProperties class defines the configuration properties for WeChat Mini Programs, containing multiple Config objects. Each Config sets parameters such as appid, secret, token, aesKey, and msgDataFormat. |



## Class WxMaProperties

|      |      |
|------|------|
| Access Modifier | @Data;@ConfigurationProperties(prefix = "wx.miniapp");public |
| Type | class |
| Name | WxMaProperties |
| Description | The WxMaProperties class defines the configuration properties for WeChat Mini Programs, containing multiple Config objects. Each Config sets parameters such as appid, secret, token, aesKey, and msgDataFormat. |


### UML Class Diagram

```mermaid
classDiagram
    class WxMaProperties {
        -List~Config~ configs
        +List~Config~ getConfigs()
        +void setConfigs(List~Config~ configs)
    }

    class Config {
        -String appid
        -String secret
        -String token
        -String aesKey
        -String msgDataFormat
        +String getAppid()
        +void setAppid(String appid)
        +String getSecret()
        +void setSecret(String secret)
        +String getToken()
        +void setToken(String token)
        +String getAesKey()
        +void setAesKey(String aesKey)
        +String getMsgDataFormat()
        +void setMsgDataFormat(String msgDataFormat)
    }

    WxMaProperties --> Config : contains
```

This code describes a WeChat Mini Program configuration class WxMaProperties, which contains a list of Config classes named configs. The Config class encapsulates core configuration items of the WeChat Mini Program, including attributes such as appid, secret, token, aesKey, and msgDataFormat. The WxMaProperties class binds to configuration files through the @ConfigurationProperties annotation, with Config as its inner static class, forming a composition relationship between the two. All fields automatically generate getter and setter methods via Lombok's @Data annotation, simplifying the code structure.


### Internal Method Call Graph

```mermaid
graph TD
    A["Class WxMaProperties"]
    B["Property: List<Config> configs"]
    C["Nested Class Config"]
    D["Property: String appid"]
    E["Property: String secret"]
    F["Property: String token"]
    G["Property: String aesKey"]
    H["Property: String msgDataFormat"]
    
    A --> B
    A -.-> C
    C --> D
    C --> E
    C --> F
    C --> G
    C --> H
```

This flowchart illustrates the structure of the WxMaProperties class and its nested Config class. As the main configuration class, WxMaProperties contains a list property named configs of type Config. The Config class defines five core configuration properties for WeChat Mini Programs: appid (application ID), secret (application secret), token (message verification token), aesKey (encryption key), and msgDataFormat (message format). Through the @ConfigurationProperties annotation, this class supports automatic injection of property values prefixed with "wx.miniapp" from configuration files.

### Field List

| Name  | Type  | Description |
|-------|-------|------|
| configs | List<Config> | Private configuration list. |

### Method List

| Name  | Type  | Description |
|-------|-------|------|




