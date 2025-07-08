[回到首页](../README.md)

## 项目概览
### 项目基本信息
- **名称:** spring-boot-demo-for-wechat-miniapp
- **GroupId (Maven):** com.github.binarywang
- **ArtifactId (Maven):** weixin-java-miniapp-demo
- **Version:** 1.0.0-SNAPSHOT
- **主要编程语言:** Java

## 先决条件
- **JDK 版本:** 1.8 (根据 Maven 的 `<maven.compiler.source>` 和 `<maven.compiler.target>` 属性推断)
- **构建工具版本:** Maven (根据 `pom.xml` 文件识别，未明确指定 Maven 版本，但建议使用与 Spring Boot 2.6.3 兼容的版本，通常为 Maven 3.6.3+)
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
    - Maven 的构建流程主要包括清理（clean）、编译（compile）、测试（test）、打包（package）、验证（verify）、安装（install）和部署（deploy）等阶段。该项目使用了 Spring Boot 和 Docker 插件，打包后会生成一个可执行的 JAR 文件，并且可以通过 Docker 插件构建 Docker 镜像。
- 打包目录: 
    - 打包后的 JAR 文件位于 `target/` 目录下，文件名为 `${project.build.finalName}.jar`（例如 `weixin-java-miniapp-demo-1.0.0-SNAPSHOT.jar`）。
    - 如果使用 Docker 插件构建镜像，Docker 相关的文件（如 Dockerfile）应放在 `src/main/docker/` 目录下，构建的镜像名称格式为 `${docker.image.prefix}/${project.artifactId}`（例如 `wx-miniapp-demo/weixin-java-miniapp-demo`）。

## 依赖管理
### 主要依赖
- **Spring Boot Web**: `spring-boot-starter-web` - 提供Spring MVC和嵌入式Tomcat支持（版本继承自父POM 2.6.3）
- **Thymeleaf**: `spring-boot-starter-thymeleaf` - 模板引擎集成（版本继承自父POM）
- **微信小程序SDK**: `weixin-java-miniapp:4.7.0` - 微信小程序Java SDK
- **文件上传**: `commons-fileupload:1.5` - Apache Commons文件上传组件
- **测试**: `spring-boot-starter-test` - Spring Boot测试支持（scope=test）
- **配置处理**: `spring-boot-configuration-processor` - 配置元数据生成（optional=true）
- **Lombok**: `lombok` - 代码简化工具（scope=provided）
- **Redis客户端**: `jedis` - Redis Java客户端（版本继承自父POM）

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
  通过父POM（`spring-boot-starter-parent:2.6.3`）集中管理依赖版本，子模块无需显式指定版本。自定义版本可通过`<properties>`（如`<weixin-java-miniapp.version>4.7.0</weixin-java-miniapp.version>`）或直接在`<dependency>`中覆盖。



## 工程结构

```text
weixin-java-miniapp-demo/
├── .editorconfig       # 编辑器配置（标准化配置）
├── .gitignore         # Git忽略规则
├── README.md          # 项目说明文档
├── .travis.yml        # CI/CD配置（Travis CI）
├── pom.xml            # Maven项目配置文件
├── commit.sh          # Git提交脚本（推测）
├── src/
│   └── main/
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # SpringBoot启动类
│       │       ├── controller/               # 微信小程序控制器
│       │       │   ├── WxMaMediaController.java  # 媒体处理接口
│       │       │   ├── WxMaUserController.java    # 用户相关接口
│       │       │   └── WxPortalController.java    # 微信消息入口
│       │       ├── utils/                    # 工具类
│       │       │   └── JsonUtils.java        # JSON处理工具
│       │       ├── error/                   # 错误处理
│       │       │   ├── ErrorController.java  # 全局异常处理
│       │       │   └── ErrorPageConfiguration.java # 错误页面配置
│       │       └── config/                   # 微信配置
│       │           ├── WxMaProperties.java   # 配置属性类
│       │           └── WxMaConfiguration.java # 微信配置类
│       ├── resources/
│       │   ├── application.yml.template      # 配置模板
│       │   ├── templates/                    # 前端模板
│       │   │   └── error.html                # 错误页面模板
│       │   └── META-INF/                     # 元数据配置
│       │       └── additional-spring-configuration-metadata.json  # Spring配置扩展
│       └── docker/
│           └── Dockerfile                    # 容器化部署配置
└── .git/                # Git版本控制目录（标准VCS结构）
```

命名规约：采用Java标准包命名（com.github.组织名），目录使用小写中划线风格
分层结构：典型SpringBoot分层，包含controller/config/utils，特别包含微信小程序专属配置层
扩展设计：通过独立docker目录支持容器化部署，META-INF提供Spring配置扩展能力