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
- **构建工具版本:** Maven (根据文件内容识别为 `pom.xml`，但未明确指定 Maven 版本，建议使用与 Spring Boot 2.6.3 兼容的版本，如 Maven 3.6.3+)
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
    - Maven 构建流程包括清理（clean）、编译（compile）、测试（test）、打包（package）、安装（install）和部署（deploy）等阶段。该项目使用了 Spring Boot 和 Docker 插件，打包后会生成一个可执行的 JAR 文件，并且可以通过 Docker 插件构建 Docker 镜像。
- 打包目录: 
    - 打包后的 JAR 文件位于 `target/` 目录下，文件名为 `${project.build.finalName}.jar`（例如 `weixin-java-miniapp-demo-1.0.0-SNAPSHOT.jar`）。
    - 如果使用 Docker 插件构建镜像，Docker 相关的文件（如 Dockerfile）应放在 `src/main/docker/` 目录下。

## 依赖管理
### 主要依赖
- **Spring Boot Web**: `spring-boot-starter-web` - 提供Spring MVC和嵌入式Tomcat支持（版本通过父POM继承）
- **Spring Boot Thymeleaf**: `spring-boot-starter-thymeleaf` - 集成Thymeleaf模板引擎（版本通过父POM继承）
- **微信小程序SDK**: `weixin-java-miniapp` - 微信小程序Java SDK（版本通过属性`${weixin-java-miniapp.version}`管理，当前为4.7.0）
- **文件上传**: `commons-fileupload` - Apache Commons文件上传组件（显式版本1.5）
- **测试**: `spring-boot-starter-test` - Spring Boot测试支持（scope为test）
- **Lombok**: `lombok` - 代码简化工具（scope为provided）
- **Redis客户端**: `jedis` - Redis Java客户端（版本通过父POM继承）

### 添加/修改依赖
- **Maven:** 在 `pom.xml` 文件的 `<dependencies>` 标签中添加或修改 `<dependency>` 元素。

### 依赖版本管理
- **Maven (`<dependencyManagement>`):**  
  1. **父POM继承**：通过`<parent>`继承`spring-boot-starter-parent`的依赖管理，自动传递版本（如Spring Boot相关依赖）。  
  2. **属性变量**：在`<properties>`中定义版本属性（如`weixin-java-miniapp.version`），通过`${property}`引用。  
  3. **显式版本**：直接在`<dependency>`中指定`<version>`（如`commons-fileupload`）。  
  4. **依赖管理标签**：若存在`<dependencyManagement>`，可集中管理依赖版本（当前文件未显式使用此标签）。



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
│       ├── resources/
│       │   ├── application.yml.template  # 应用配置模板
│       │   ├── tmp.png                  # 临时图片资源（推测）
│       │   ├── templates/
│       │   │   └── error.html           # 错误页面模板
│       │   └── META-INF/
│       │       └── additional-spring-configuration-metadata.json  # Spring配置元数据
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # Spring Boot启动类
│       │       ├── controller/
│       │       │   ├── WxMaMediaController.java  # 微信媒体控制器
│       │       │   ├── WxMaUserController.java   # 微信用户控制器
│       │       │   └── WxPortalController.java   # 微信入口控制器
│       │       ├── utils/
│       │       │   └── JsonUtils.java            # JSON工具类
│       │       ├── error/
│       │       │   ├── ErrorController.java       # 错误处理控制器
│       │       │   └── ErrorPageConfiguration.java # 错误页面配置
│       │       └── config/
│       │           ├── WxMaProperties.java        # 微信配置属性
│       │           └── WxMaConfiguration.java     # 微信配置类
│       └── docker/
│           └── Dockerfile                # 容器化部署配置
├── .git/                # Git版本控制目录（标准结构）
└── .github/
    └── FUNDING.yml      # GitHub赞助配置
```

命名规约：采用Java标准包命名（com.github.*）和kebab-case风格（如.editorconfig）
分层结构：标准Spring Boot分层，包含controller/config/utils等模块，resources目录存放静态资源和配置
扩展设计：通过独立的docker目录支持容器化部署，.github目录支持社区生态功能