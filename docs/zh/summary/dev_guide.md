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
- **构建工具版本:** Maven (根据 `pom.xml` 文件识别)
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
    - Maven 的构建流程主要包括以下阶段：清理（clean）、编译（compile）、测试（test）、打包（package）、验证（verify）、安装（install）、部署（deploy）。本项目使用了 Spring Boot 的 Maven 插件，打包后会生成一个可执行的 JAR 文件。
- 打包目录: 
    - 打包后的文件默认位于 `target/` 目录下，文件名为 `${project.build.finalName}.jar`（例如 `weixin-java-miniapp-demo-1.0.0-SNAPSHOT.jar`）。
    - 如果启用了 Docker 插件，Docker 相关的文件位于 `src/main/docker/` 目录下。

## 依赖管理
### 主要依赖
- **Spring Boot Starter Web**: 用于构建基于Spring的Web应用程序 (版本继承自父POM 2.6.3)
- **Spring Boot Starter Thymeleaf**: 集成Thymeleaf模板引擎 (版本继承自父POM)
- **weixin-java-miniapp**: 微信小程序Java SDK (版本4.7.0通过属性`weixin-java-miniapp.version`管理)
- **commons-fileupload**: 文件上传组件 (显式指定版本1.5)
- **Spring Boot Starter Test**: 测试支持 (版本继承自父POM，scope为test)
- **Lombok**: 注解驱动的代码生成工具 (scope为provided)
- **Jedis**: Redis Java客户端 (版本继承自父POM)

### 添加/修改依赖
- **Maven:** 在 `pom.xml` 文件的 `<dependencies>` 标签中添加或修改 `<dependency>` 元素。

### 依赖版本管理
- **Maven (`<dependencyManagement>`):** 
  1. 通过父POM (`spring-boot-starter-parent`) 集中管理大部分依赖版本
  2. 自定义属性管理特定依赖版本 (如`<weixin-java-miniapp.version>4.7.0</weixin-java-miniapp.version>`)
  3. 未指定版本时继承父POM版本，显式声明版本会覆盖继承值



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
│       │   ├── tmp.png                   # 临时图片资源（推测）
│       │   ├── templates/
│       │   │   └── error.html           # 错误页面模板
│       │   └── META-INF/
│       │       └── additional-spring-configuration-metadata.json  # Spring配置元数据
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # Spring Boot启动类
│       │       ├── controller/
│       │       │   ├── WxMaMediaController.java  # 微信媒体接口控制器
│       │       │   ├── WxMaUserController.java   # 微信用户接口控制器
│       │       │   └── WxPortalController.java   # 微信入口控制器
│       │       ├── utils/
│       │       │   └── JsonUtils.java      # JSON工具类
│       │       ├── error/
│       │       │   ├── ErrorController.java       # 错误处理控制器
│       │       │   └── ErrorPageConfiguration.java  # 错误页面配置
│       │       └── config/
│       │           ├── WxMaProperties.java    # 微信小程序配置属性
│       │           └── WxMaConfiguration.java # 微信小程序配置类
│       └── docker/
│           └── Dockerfile  # 容器化部署配置
└── .github/
    └── FUNDING.yml         # GitHub赞助配置
```

命名规约：采用标准Java包命名规范（com.github.组织名.项目名），目录使用小写短横线风格（如miniapp）

分层结构：
1. 控制层：controller包处理微信接口请求
2. 工具层：utils包提供JSON序列化能力
3. 配置层：config包管理微信SDK配置
4. 错误处理：独立error包实现全局异常处理
5. 资源层：resources目录包含静态资源和模板

扩展设计：
1. 通过独立的docker目录支持容器化部署
2. 配置模板机制（application.yml.template）
3. 完善的错误处理体系（错误控制器+页面模板）
4. CI/CD集成（.travis.yml）
5. 标准化Spring配置元数据（META-INF）