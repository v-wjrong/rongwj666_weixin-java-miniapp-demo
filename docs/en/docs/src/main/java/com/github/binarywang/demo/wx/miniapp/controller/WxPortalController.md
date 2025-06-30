# Basic Information

|      |      |
|------|------|
| Name | WxPortalController |
| Language | .java |
| Code Path | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo/wx/miniapp/controller/WxPortalController.java |
| Package Name | com.github.binarywang.demo.wx.miniapp.controller |
| Dependencies | ['cn.binarywang.wx.miniapp.api.WxMaService', 'cn.binarywang.wx.miniapp.bean.WxMaMessage', 'cn.binarywang.wx.miniapp.constant.WxMaConstants', 'cn.binarywang.wx.miniapp.message.WxMaMessageRouter', 'cn.binarywang.wx.miniapp.util.WxMaConfigHolder', 'lombok.AllArgsConstructor', 'lombok.extern.slf4j.Slf4j', 'org.apache.commons.lang3.StringUtils', 'org.springframework.web.bind.annotation', 'java.util.Objects'] |
| Brief Description | WeChat Mini Program controller class, handling GET/POST requests, verifying signatures, and routing messages. GET is used for authentication, POST processes plaintext or AES-encrypted messages, verifies the appid, forwards the message, and returns the result. Clears ThreadLocal after each request. |

# Description

This is a backend controller class for a WeChat Mini Program, containing two main interfaces. The GET interface is used for WeChat server authentication, verifying the signature parameters and returning the echostr string. The POST interface handles WeChat message requests, supporting both plaintext and AES-encrypted formats. It parses the message based on its format, routes it for processing, and returns a success response. Both interfaces check the validity of the appid and clean up the configuration information stored in ThreadLocal after processing.

# Class Summary

| Name   | Type  | Description |
|-------|------|-------------|
| WxPortalController | class | WeChat Mini Program Controller, handling authentication and message requests, verifying signatures and routing messages, supporting plaintext and AES encryption, returning success or error messages. |



## Class WxPortalController

|      |      |
|------|------|
| Access Modifier | @RestController;@AllArgsConstructor;@RequestMapping("/wx/portal/{appid}");@Slf4j;public |
| Type | class |
| Name | WxPortalController |
| Description | WeChat Mini Program Controller, handling authentication and message requests, verifying signatures and routing messages, supporting plaintext and AES encryption, returning success or error messages. |


### UML Class Diagram

```mermaid
classDiagram
    class WxPortalController {
        -WxMaService wxMaService
        -WxMaMessageRouter wxMaMessageRouter
        +authGet(String appid, String signature, String timestamp, String nonce, String echostr) String
        +post(String appid, String requestBody, String msgSignature, String encryptType, String signature, String timestamp, String nonce) String
        -route(WxMaMessage message) void
    }

    class WxMaService {
        <<Interface>>
        +switchover(String appid) boolean
        +checkSignature(String timestamp, String nonce, String signature) boolean
        +getWxMaConfig() WxMaConfig
    }

    class WxMaMessageRouter {
        +route(WxMaMessage message) void
    }

    class WxMaMessage {
        <<Interface>>
        +fromJson(String json) WxMaMessage
        +fromXml(String xml) WxMaMessage
        +fromEncryptedJson(String json, WxMaConfig config) WxMaMessage
        +fromEncryptedXml(String xml, WxMaConfig config, String timestamp, String nonce, String msgSignature) WxMaMessage
    }

    class WxMaConfig {
        +getMsgDataFormat() String
    }

    class WxMaConfigHolder {
        +remove() void
    }

    class WxMaConstants {
        <<Enumeration>>
        +MsgDataFormat JSON
        +MsgDataFormat XML
    }

    WxPortalController --> WxMaService : Dependency
    WxPortalController --> WxMaMessageRouter : Dependency
    WxMaMessageRouter --> WxMaMessage : Process
    WxMaService --> WxMaConfig : Get Config
    WxMaMessage --> WxMaConfig : Dependency
    WxPortalController --> WxMaConfigHolder : Clean ThreadLocal
    WxMaService --> WxMaConstants : Use Enum
```

Class Diagram Description:
This diagram illustrates the core structure of a WeChat Mini Program Portal Controller (WxPortalController), which handles WeChat server authentication and message encryption/decryption through WxMaService, and routes messages using WxMaMessageRouter. The controller exposes two public methods (GET/POST) for processing verification requests and message pushes respectively, relying on WxMaConfigHolder to manage thread-local variables. The system adheres to the interface segregation principle, with WxMaService and WxMaMessage as key interfaces supporting both JSON/XML data formats, while maintaining constants via the WxMaConstants enumeration. The overall architecture demonstrates clear responsibility division and modular design.


### Internal Method Call Graph

```mermaid
graph TD
    A["WxPortalController Class"]
    B["GET Authentication Flow: authGet"]
    C["POST Message Handling: post"]
    D["Routing Method: route"]
    E["Dependency Service: wxMaService"]
    F["Dependency Router: wxMaMessageRouter"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F

    B --> B1["Log Request"]
    B --> B2{"Parameter Validation"}
    B2 -->|Invalid| B3["Throw Exception"]
    B2 -->|Valid| B4{"Switch appid Configuration"}
    B4 -->|Failed| B5["Throw Exception"]
    B4 -->|Success| B6{"Verify Signature"}
    B6 -->|Valid| B7["Return echostr"]
    B6 -->|Invalid| B8["Return 'Invalid Request'"]
    B7 & B8 --> B9["Clean ThreadLocal"]

    C --> C1["Log Request"]
    C --> C2{"Switch appid Configuration"}
    C2 -->|Failed| C3["Throw Exception"]
    C2 -->|Success| C4{"Encryption Type Check"}
    C4 -->|Plaintext| C5["Parse JSON/XML"]
    C4 -->|AES Encrypted| C6["Decrypt JSON/XML"]
    C4 -->|Other| C7["Throw Exception"]
    C5 & C6 --> C8["Route Message"]
    C8 --> C9["Return 'success'"]
    C9 & C7 --> C10["Clean ThreadLocal"]
```

```mermaid
sequenceDiagram
    participant Client as WeChat Client
    participant Controller as WxPortalController
    participant Service as wxMaService
    participant Router as wxMaMessageRouter

    Note over Client,Router: GET Authentication Flow
    Client->>Controller: GET Request with Parameters
    Controller->>Controller: Log Request
    Controller->>Controller: Validate Parameters
    alt Invalid Parameters
        Controller-->>Client: Throw Exception
    else Valid Parameters
        Controller->>Service: switchover(appid)
        alt Configuration Missing
            Controller-->>Client: Throw Exception
        else Configuration Exists
            Controller->>Service: checkSignature()
            alt Signature Valid
                Controller-->>Client: Return echostr
            else Signature Invalid
                Controller-->>Client: Return 'Invalid Request'
            end
        end
    end
    Controller->>Controller: Clean ThreadLocal

    Note over Client,Router: POST Message Handling
    Client->>Controller: POST Request with Parameters
    Controller->>Controller: Log Request
    Controller->>Service: switchover(appid)
    alt Configuration Missing
        Controller-->>Client: Throw Exception
    else Configuration Exists
        alt Plaintext Message
            Controller->>Controller: Parse JSON/XML
            Controller->>Router: route(message)
            Controller-->>Client: Return 'success'
        else AES Encrypted Message
            Controller->>Controller: Decrypt JSON/XML
            Controller->>Router: route(message)
            Controller-->>Client: Return 'success'
        else Unknown Encryption Type
            Controller-->>Client: Throw Exception
        end
    end
    Controller->>Controller: Clean ThreadLocal
```

The flowchart and sequence diagram illustrate the complete processing logic of a WeChat Mini Program backend controller. The GET authentication flow includes three key stages: parameter validation, configuration switching, and signature verification. The POST message handling distinguishes between plaintext and encrypted message types for different processing. Both flows incorporate a ThreadLocal cleanup mechanism to ensure thread safety. The sequence diagram clearly presents the interaction sequence and conditional branches between the client, controller, and service components, fully covering the authentication and message handling scenarios for WeChat message push.

### Field List

| Name  | Type  | Description |
|-------|-------|------|
| wxMaService | WxMaService | WeChat Mini Program service instance, private and immutable. |
| wxMaMessageRouter | WxMaMessageRouter | Private immutable instance of the WeChat Mini Program message router. |

### Method List

| Name  | Type  | Description |
|-------|-------|------|
| route | void | The method `route` processes WeChat messages, invokes the routing functionality, and captures exceptions to log them. |
| post | String | POST interface for handling WeChat requests, verifying appid and parsing plaintext or AES-encrypted XML/JSON messages, returning "success" after processing, and clearing ThreadLocal while reporting errors in case of exceptions. |
| authGet | String | This is a GET interface for handling WeChat server authentication requests, which verifies the signature parameters and returns the echostr or an error message. |




