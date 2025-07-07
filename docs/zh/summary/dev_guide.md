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
  - Redis (通过 `jedis` 依赖引入，未明确指定版本，由 Spring Boot 父 POM 管理)

## 构建指南
### Maven 构建
- 构建命令:
    - 清理构建: `mvn clean`
    - 编译项目: `mvn compile`
    - 打包项目: `mvn package`
    - 安装到本地仓库: `mvn install`
    - 部署项目: `mvn deploy`
- 构建流程: 
    - Maven 的构建流程主要包括清理（clean）、编译（compile）、测试（test）、打包（package）、安装（install）和部署（deploy）等阶段。该项目使用了 Spring Boot 的 Maven 插件，因此打包后会生成一个可执行的 JAR 文件。
- 打包目录: 
    - 打包后的 JAR 文件位于 `target` 目录下，文件名为 `${project.artifactId}-${project.version}.jar`。如果使用了 Docker 插件，Docker 相关的配置和资源文件位于 `src/main/docker` 目录下。

## 依赖管理
### 主要依赖
- **Spring Boot Web**: `spring-boot-starter-web` - 提供 Spring MVC 和嵌入式 Tomcat 支持（版本通过父 POM 继承，未显式指定）。
- **Thymeleaf**: `spring-boot-starter-thymeleaf` - 模板引擎集成（版本继承自父 POM）。
- **微信小程序 SDK**: `weixin-java-miniapp` - 微信小程序 Java SDK（版本通过属性 `${weixin-java-miniapp.version}` 管理，当前为 `4.7.0`）。
- **文件上传**: `commons-fileupload` - Apache Commons 文件上传组件（显式版本 `1.5`）。
- **测试**: `spring-boot-starter-test` - Spring Boot 测试支持（`test` 作用域）。
- **Lombok**: `lombok` - 代码生成工具（`provided` 作用域）。
- **Redis 客户端**: `jedis` - Redis Java 客户端（版本继承自父 POM）。

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
  依赖版本可通过以下方式管理：
  1. **父 POM 继承**（如本例中 `spring-boot-starter-parent` 统一管理 Spring Boot 相关依赖版本）。
  2. **`<properties>` 标签**定义版本变量（如 `${weixin-java-miniapp.version}`）。
  3. **显式 `<version>` 标签**直接指定版本（如 `commons-fileupload`）。
  4. **`<dependencyManagement>` 块**集中管理依赖版本（本例未使用，但常见于多模块项目）。



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
│       │   ├── application.yml.template  # Spring Boot配置模板
│       │   ├── tmp.png                   # 临时图片资源（推测）
│       │   ├── templates/
│       │   │   └── error.html           # 错误页面模板
│       │   └── META-INF/
│       │       └── additional-spring-configuration-metadata.json  # Spring配置元数据
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # Spring Boot启动类
│       │       ├── controller/               # 微信小程序控制器
│       │       │   ├── WxMaMediaController.java   # 媒体处理控制器
│       │       │   ├── WxMaUserController.java    # 用户管理控制器
│       │       │   └── WxPortalController.java    # 入口控制器
│       │       ├── utils/                    # 工具类
│       │       │   └── JsonUtils.java        # JSON处理工具
│       │       ├── error/                    # 错误处理模块
│       │       │   ├── ErrorController.java      # 全局错误控制器
│       │       │   └── ErrorPageConfiguration.java  # 错误页面配置
│       │       └── config/                   # 微信配置模块
│       │           ├── WxMaProperties.java       # 微信配置属性
│       │           └── WxMaConfiguration.java    # 微信配置类
│       └── docker/
│           └── Dockerfile                # 容器化部署配置
├── .git/                                # Git版本控制目录（标准VCS结构）
└── .github/                             # GitHub平台配置
    └── FUNDING.yml                      # GitHub赞助配置
```

命名规约：采用Java标准包命名（com.github.组织名），目录使用小写短横线风格（如miniapp-demo）

分层结构：
1. 控制层：controller处理微信接口请求
2. 配置层：config管理微信SDK配置
3. 工具层：utils提供JSON序列化能力
4. 错误处理层：error实现全局异常拦截
5. 资源层：resources包含静态模板和配置

扩展设计：
1. 通过独立的docker目录支持容器化部署
2. 配置模板(application.yml.template)实现环境隔离
3. .travis.yml提供持续集成扩展点
4. META-INF支持Spring Boot配置扩展