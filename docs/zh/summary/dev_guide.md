[回到首页](../README.md)

## 项目概览
### 项目基本信息
- **名称:** spring-boot-demo-for-wechat-miniapp
- **GroupId (Maven):** com.github.binarywang
- **ArtifactId (Maven):** weixin-java-miniapp-demo
- **Version:** 1.0.0-SNAPSHOT
- **主要编程语言:** Java

## 先决条件
- **JDK 版本:** 1.8 (根据 Maven 编译器配置 `<maven.compiler.source>` 和 `<maven.compiler.target>`)
- **构建工具版本:** Maven (根据 `pom.xml` 文件结构和内容识别)
- **网络连接中间件依赖:**
  - Redis (通过 `jedis` 依赖推断，版本未明确指定)

## 构建指南
### Maven 构建
- 构建命令:
    - 清理构建: `mvn clean`
    - 编译项目: `mvn compile`
    - 打包项目: `mvn package`
    - 安装到本地仓库: `mvn install`
    - 部署项目: `mvn deploy`
- 构建流程: 
    - Maven 的构建流程主要包括以下阶段：
        1. 清理 (clean): 删除之前构建生成的文件
        2. 编译 (compile): 编译项目源代码
        3. 测试 (test): 运行单元测试
        4. 打包 (package): 将编译后的代码打包成可分发的格式（如 JAR）
        5. 验证 (verify): 运行任何检查以验证包是否有效
        6. 安装 (install): 将包安装到本地仓库
        7. 部署 (deploy): 将最终包复制到远程仓库
- 打包目录: 
    - 构建后的文件默认位于 `target/` 目录下
    - 最终打包的 JAR 文件名为 `${artifactId}-${version}.jar`（如 `weixin-java-miniapp-demo-1.0.0-SNAPSHOT.jar`）
    - 该项目还配置了 Docker 构建插件，Docker 相关文件位于 `src/main/docker` 目录

## 依赖管理
### 主要依赖
- **Spring Boot 基础依赖**:
  - `spring-boot-starter-web`: Web 应用支持 (版本继承自父 POM 2.6.3)
  - `spring-boot-starter-thymeleaf`: Thymeleaf 模板引擎集成
  - `spring-boot-starter-test`: 测试支持 (scope=test)
  - `spring-boot-configuration-processor`: 配置元数据生成 (optional=true)
- **微信小程序 SDK**:
  - `weixin-java-miniapp`: 微信小程序 Java SDK (版本通过属性 `${weixin-java-miniapp.version}` 管理，当前为 4.7.0)
- **工具库**:
  - `commons-fileupload`: 文件上传功能 (版本 1.5)
  - `lombok`: 代码简化工具 (scope=provided)
  - `jedis`: Redis 客户端 (版本继承自 Spring Boot 依赖管理)

### 添加/修改依赖
- **Maven:** 在 `pom.xml` 文件的 `<dependencies>` 标签中添加或修改 `<dependency>` 元素，例如：
  ```xml
  <dependency>
      <groupId>org.example</groupId>
      <artifactId>new-dependency</artifactId>
      <version>1.0.0</version>
  </dependency>
  ```

### 依赖版本管理
- **Maven (`<dependencyManagement>`):**  
  该文件通过父 POM (`spring-boot-starter-parent`) 集中管理大部分依赖版本（如 Spring Boot 相关依赖）。自定义版本可通过：
  1. `<properties>` 标签定义变量（如 `${weixin-java-miniapp.version}`）
  2. 直接在 `<dependency>` 中显式指定 `<version>`
  3. 使用 `<dependencyManagement>` 覆盖父 POM 的版本管理



## 工程结构

```text
weixin-java-miniapp-demo/
├── .editorconfig        # 编辑器配置（标准化配置）
├── .gitignore          # Git忽略规则
├── README.md           # 项目说明文档
├── .travis.yml         # CI/CD配置（Travis CI）
├── pom.xml             # Maven项目配置文件
├── commit.sh           # Git提交脚本（推测）
├── src/
│   └── main/
│       ├── resources/
│       │   ├── application.yml.template  # Spring Boot配置模板
│       │   ├── tmp.png                  # 临时图片资源（推测）
│       │   ├── templates/
│       │   │   └── error.html          # 错误页面模板
│       │   └── META-INF/
│       │       └── additional-spring-configuration-metadata.json  # Spring配置元数据
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # Spring Boot主类
│       │       ├── controller/
│       │       │   ├── WxMaMediaController.java   # 微信媒体API控制器
│       │       │   ├── WxMaUserController.java    # 微信用户API控制器
│       │       │   └── WxPortalController.java    # 微信入口控制器
│       │       ├── utils/
│       │       │   └── JsonUtils.java            # JSON工具类
│       │       ├── error/
│       │       │   ├── ErrorController.java       # 全局错误处理
│       │       │   └── ErrorPageConfiguration.java # 错误页面配置
│       │       └── config/
│       │           ├── WxMaProperties.java       # 微信配置属性类
│       │           └── WxMaConfiguration.java    # 微信配置类
│       └── docker/
│           └── Dockerfile              # 容器化部署配置
├── .git/                # Git版本控制目录（标准VCS结构）
└── .github/
    └── FUNDING.yml      # GitHub赞助配置
```

命名规约：采用全小写+中划线风格（如wx-miniapp），Java包路径符合域名反转规范（com.github.binarywang）
分层结构：标准Spring Boot分层，包含controller层（API入口）、config层（配置管理）、utils层（工具类），通过error目录实现全局异常处理
扩展设计：通过独立的docker目录支持容器化部署，resources/templates实现前端页面分离，META-INF支持Spring配置扩展