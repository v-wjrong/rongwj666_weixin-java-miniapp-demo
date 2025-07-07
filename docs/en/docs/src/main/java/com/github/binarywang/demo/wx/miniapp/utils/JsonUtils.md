# Basic Information

|      |      |
|------|------|
| Name | JsonUtils |
| Language | .java |
| Code Path | weixin-java-miniapp-demo/src/main/java/com/github/binarywang/demo/wx/miniapp/utils/JsonUtils.java |
| Package Name | com.github.binarywang.demo.wx.miniapp.utils |
| Dependencies | ['com.fasterxml.jackson.annotation.JsonInclude.Include', 'com.fasterxml.jackson.core.JsonProcessingException', 'com.fasterxml.jackson.databind.ObjectMapper', 'com.fasterxml.jackson.databind.SerializationFeature'] |
| Brief Description | The JsonUtils class provides a static method `toJson`, which uses ObjectMapper to convert an object into a JSON string, automatically ignoring null values and formatting the output. |

# Description

JsonUtils is a utility class designed for handling JSON serialization. It utilizes ObjectMapper as its core component and configures two key options in the static initialization block: ignoring null fields and enabling indented formatting for output. The class provides a static method `toJson` to convert any object into a JSON string. If a JsonProcessingException occurs during the conversion, the exception stack trace will be printed, and null will be returned. The entire class is designed to be a concise and practical JSON serialization tool.

# Class Summary

| Name   | Type  | Description |
|-------|------|-------------|
| JsonUtils | class | The JsonUtils class provides a static method `toJson`, which uses ObjectMapper to convert an object into a JSON string, ignoring null values and formatting the output. Returns null if an exception occurs. |



## Class JsonUtils

|      |      |
|------|------|
| Access Modifier | public |
| Type | class |
| Name | JsonUtils |
| Description | The JsonUtils class provides a static method `toJson`, which uses ObjectMapper to convert an object into a JSON string, ignoring null values and formatting the output. Returns null if an exception occurs. |


### UML Class Diagram

```mermaid
classDiagram
    class JsonUtils {
        -ObjectMapper JSON
        ..
        +String toJson(Object obj)
    }
    class ObjectMapper {
        <<SerializationFeature>>
        +setSerializationInclusion(Include inclusion)
        +configure(SerializationFeature feature, Boolean enabled)
        +String writeValueAsString(Object obj) throws JsonProcessingException
    }
    class Include {
        <<enumeration>>
        NON_NULL
    }
    class SerializationFeature {
        <<enumeration>>
        INDENT_OUTPUT
    }
    JsonUtils --> ObjectMapper : dependency
    ObjectMapper --> Include : uses
    ObjectMapper --> SerializationFeature : uses
```

This code demonstrates a JSON utility class `JsonUtils` that utilizes `ObjectMapper` for object serialization operations. The class diagram consists of four main components: `JsonUtils` serves as a utility class encapsulating the core method `toJson()`; `ObjectMapper` is the core serialization class from the Jackson library, configured with non-null value filtering and indented output features; `Include` and `SerializationFeature` are enumeration types used to configure serialization behaviors. The overall structure reflects the encapsulation pattern of a utility class around a third-party library, with global configurations applied through static initialization blocks and handling of potential `JsonProcessingException` exceptions.


### Internal Method Call Graph

```mermaid
graph TD
    A["Class JsonUtils"]
    B["Static Property: ObjectMapper JSON"]
    C["Static Initialization Block"]
    D["Setting: JSON.setSerializationInclusion(Include.NON_NULL)"]
    E["Configuration: JSON.configure(SerializationFeature.INDENT_OUTPUT, Boolean.TRUE)"]
    F["Static Method: String toJson(Object obj)"]
    G["Execution: JSON.writeValueAsString(obj)"]
    H["Exception Handling: JsonProcessingException e"]
    I["Exception Processing: e.printStackTrace()"]
    J["Return null"]

    A --> B
    A --> C
    C --> D
    C --> E
    A --> F
    F --> G
    G -->|Exception| H
    H --> I
    I --> J
    G -->|Normal| F
```

This code flowchart illustrates the structure and workflow of the JsonUtils utility class. The class implements JSON serialization functionality through a static ObjectMapper instance, configured in the static initialization block to ignore null values and enable pretty-printing. The core method toJson converts objects to JSON strings via writeValueAsString, while handling potential JsonProcessingException exceptions. The flowchart clearly presents the complete path from class initialization to method invocation, including both normal flow and exception handling branches.

### Field List

| Name  | Type  | Description |
|-------|-------|------|
| JSON = new ObjectMapper() | ObjectMapper | Define a private static immutable JSON object mapper instance. |

### Method List

| Name  | Type  | Description |
|-------|-------|------|
| toJson | String | Convert the object to a JSON string, return null if failed. |




