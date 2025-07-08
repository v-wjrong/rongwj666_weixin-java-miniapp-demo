[回到首页](../README.md)

## 项目概览
### 项目基本信息
- **名称:** spring-boot-demo-for-wechat-miniapp
- **GroupId (Maven):** com.github.binarywang
- **ArtifactId (Maven):** weixin-java-miniapp-demo
- **Version:** 1.0.0-SNAPSHOT
- **主要编程语言:** Java

## 先决条件
- **JDK 版本:** 1.8 (根据 Maven 的 `<maven.compiler.source>` 和 `<maven.compiler.target>` 属性)
- **构建工具版本:** Maven (根据 `pom.xml` 文件结构识别)
- **网络连接中间件依赖:**
  - Redis (通过 `jedis` 依赖推断，但未明确指定版本)

## 构建指南
### Maven 构建
- 构建命令:
    - 清理构建: `mvn clean`
    - 编译项目: `mvn compile`
    - 打包项目: `mvn package`
    - 安装到本地仓库: `mvn install`
    - 部署项目: `mvn deploy`
- 构建流程: 
    - Maven 的构建流程主要包括清理、编译、测试、打包、验证、安装和部署等阶段。该项目使用了 Spring Boot 和 Docker 插件，因此构建时会生成可执行的 JAR 文件，并支持 Docker 镜像构建。
- 打包目录: 
    - 打包后的 JAR 文件默认位于 `target/` 目录下，文件名为 `${project.build.finalName}.jar`（例如 `weixin-java-miniapp-demo-1.0.0-SNAPSHOT.jar`）。
    - 如果启用了 Docker 插件，Docker 镜像会根据配置生成，镜像名称为 `${docker.image.prefix}/${project.artifactId}`（例如 `wx-miniapp-demo/weixin-java-miniapp-demo`），Dockerfile 位于 `src/main/docker` 目录。

## 依赖管理
### 主要依赖
- **Spring Boot Web**: `org.springframework.boot:spring-boot-starter-web` - 提供Spring MVC和嵌入式Tomcat支持（版本通过父POM继承，未显式指定）。
- **Spring Boot Thymeleaf**: `org.springframework.boot:spring-boot-starter-thymeleaf` - 集成Thymeleaf模板引擎（版本通过父POM继承）。
- **微信小程序SDK**: `com.github.binarywang:weixin-java-miniapp:4.7.0` - 微信小程序Java SDK（通过属性`weixin-java-miniapp.version`管理版本）。
- **文件上传工具**: `commons-fileupload:commons-fileupload:1.5` - Apache Commons文件上传组件。
- **测试依赖**: `org.springframework.boot:spring-boot-starter-test` - Spring Boot测试支持（`test`作用域）。
- **Lombok**: `org.projectlombok:lombok` - 注解驱动的代码生成工具（`provided`作用域）。
- **Redis客户端**: `redis.clients:jedis` - Jedis Redis客户端（版本通过父POM继承）。

### 添加/修改依赖
- **Maven:** 在 `pom.xml` 文件的 `<dependencies>` 标签中添加或修改 `<dependency>` 元素。例如：
  ```xml
  <dependency>
      <groupId>org.example</groupId>
      <artifactId>new-dependency</artifactId>
      <version>1.0.0</version>
  </dependency>
  ```

### 依赖版本管理
- **Maven (`<dependencyManagement>`):**  
  此项目通过父POM（`spring-boot-starter-parent:2.6.3`）集中管理大部分依赖版本，例如Spring Boot相关依赖。自定义依赖版本可通过`<properties>`（如`weixin-java-miniapp.version`）或直接在`<dependency>`中指定。若需统一管理版本，可在`<dependencyManagement>`中声明。



## 工程结构

```text
weixin-java-miniapp-demo/
├── .editorconfig       # 编辑器配置（标准化配置）
├── .gitignore         # Git忽略规则
├── README.md          # 项目说明文档
├── .travis.yml        # CI/CD配置（Travis CI）
├── pom.xml            # Maven项目配置
├── commit.sh          # Git提交脚本（推测）
├── src/
│   └── main/
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # SpringBoot启动类
│       │       ├── controller/                # 微信小程序控制器
│       │       │   ├── WxMaMediaController.java  # 媒体处理接口
│       │       │   ├── WxMaUserController.java   # 用户相关接口
│       │       │   └── WxPortalController.java   # 入口验证接口
│       │       ├── utils/                     # 工具类
│       │       │   └── JsonUtils.java         # JSON处理工具
│       │       ├── error/                     # 错误处理
│       │       │   ├── ErrorController.java      # 错误控制器
│       │       │   └── ErrorPageConfiguration.java # 错误页面配置
│       │       └── config/                    # 微信配置
│       │           ├── WxMaProperties.java    # 配置属性类
│       │           ├── WxMaConfiguration.java # 微信配置类
│       │           └── ResourcesConfig.java   # 资源文件配置
│       ├── resources/
│       │   ├── application.yml.template       # 应用配置模板
│       │   ├── templates/                    # 前端模板
│       │   │   └── error.html                # 错误页面模板
│       │   └── META-INF/                     # 元数据配置
│       │       └── additional-spring-configuration-metadata.json  # Spring配置元数据
│       └── docker/
│           └── Dockerfile                    # 容器化部署配置
└── .git/               # Git版本控制目录（标准VCS结构）
```

命名规约：采用标准Java包命名（com.github.*三级域名反写）和驼峰式类名
分层结构：SpringBoot标准分层，包含config/controller/utils，特别包含微信小程序专用配置层
扩展设计：通过独立docker目录支持容器化部署，resources/META-INF提供Spring配置扩展能力