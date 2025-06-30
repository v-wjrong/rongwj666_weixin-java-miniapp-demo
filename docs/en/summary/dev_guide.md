[Go to Homepage](../README.md)

## Project Overview
### Basic Project Information
- **Name:** spring-boot-demo-for-wechat-miniapp
- **GroupId (Maven):** com.github.binarywang
- **ArtifactId (Maven):** weixin-java-miniapp-demo
- **Version:** 1.0.0-SNAPSHOT
- **Primary Programming Language:** Java

## Prerequisites
- **JDK Version:** 1.8 (inferred from Maven's `<maven.compiler.source>` and `<maven.compiler.target>` properties)
- **Build Tool Version:** Maven (identified from `pom.xml` file)
- **Network Middleware Dependencies:**
  - Redis (inferred from `jedis` dependency, but version not explicitly specified)

## Build Guide
### Maven Build
- Build Commands:
    - Clean build: `mvn clean`
    - Compile project: `mvn compile`
    - Package project: `mvn package`
    - Install to local repository: `mvn install`
    - Deploy project: `mvn deploy`
- Build Process:
    - Maven's build process mainly includes phases such as clean, compile, test, package, install, and deploy. This project uses the Spring Boot Maven plugin, so an executable JAR file will be generated after packaging.
- Packaging Directory:
    - The packaged files will be located in the `target` directory, with the filename `${project.artifactId}-${project.version}.jar` (e.g., `weixin-java-miniapp-demo-1.0.0-SNAPSHOT.jar`).
    - If the Docker plugin is used, Docker-related configuration and resource files are located in the `src/main/docker` directory.

## Dependency Management
### Main Dependencies
- **Spring Boot Web:** `org.springframework.boot:spring-boot-starter-web` - Provides Spring MVC and embedded Tomcat support (version inherited from parent POM 2.6.3)
- **Thymeleaf Template Engine:** `org.springframework.boot:spring-boot-starter-thymeleaf` - Web page rendering (version inherited from parent POM)
- **WeChat Mini Program SDK:** `com.github.binarywang:weixin-java-miniapp:4.7.0` - WeChat Mini Program Java SDK
- **File Upload:** `commons-fileupload:commons-fileupload:1.5` - Apache Commons file upload component
- **Test Support:** `org.springframework.boot:spring-boot-starter-test` - Testing framework (scope=test)
- **Configuration Processing:** `org.springframework.boot:spring-boot-configuration-processor` - Configuration metadata generation (optional=true)
- **Lombok:** `org.projectlombok:lombok` - Code simplification tool (scope=provided)
- **Redis Client:** `redis.clients:jedis` - Redis Java client (version inherited from parent POM)

### Adding/Modifying Dependencies
- **Maven:** Add or modify `<dependency>` elements within the `<dependencies>` tag in the `pom.xml` file. For example:
  ```xml
  <dependency>
      <groupId>org.example</groupId>
      <artifactId>new-dependency</artifactId>
      <version>1.0.0</version>
  </dependency>
  ```

### Dependency Version Management
- **Maven (`<dependencyManagement>`):**
  1. Parent POM (`spring-boot-starter-parent 2.6.3`) centrally manages most Spring Boot-related dependency versions.
  2. Custom versions are defined via `<properties>` (e.g., `<weixin-java-miniapp.version>4.7.0</weixin-java-miniapp.version>`).
  3. If no version is specified, the version managed by the parent POM is used first, followed by the version resolved from transitive dependencies.

## Project Structure

```text
weixin-java-miniapp-demo/
├── .editorconfig        # Editor configuration (standardized settings)
├── .gitignore          # Git ignore rules
├── README.md           # Project documentation
├── .travis.yml         # CI/CD configuration (Travis CI)
├── pom.xml             # Maven project configuration file
├── commit.sh           # Git commit script (presumed)
├── src/
│   └── main/
│       ├── resources/
│       │   ├── application.yml.template  # Spring Boot configuration template
│       │   ├── tmp.png                  # Temporary image resource (presumed)
│       │   ├── templates/
│       │   │   └── error.html          # Error page template
│       │   └── META-INF/
│       │       └── additional-spring-configuration-metadata.json  # Spring configuration metadata
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # Spring Boot main class
│       │       ├── controller/
│       │       │   ├── WxMaMediaController.java   # WeChat media API controller
│       │       │   ├── WxMaUserController.java    # WeChat user API controller
│       │       │   └── WxPortalController.java    # WeChat entry controller
│       │       ├── utils/
│       │       │   └── JsonUtils.java            # JSON utility class
│       │       ├── error/
│       │       │   ├── ErrorController.java       # Global error handling
│       │       │   └── ErrorPageConfiguration.java # Error page configuration
│       │       └── config/
│       │           ├── WxMaProperties.java       # WeChat configuration properties class
│       │           └── WxMaConfiguration.java    # WeChat configuration class
│       └── docker/
│           └── Dockerfile              # Containerized deployment configuration
├── .git/                # Git version control directory (standard VCS structure)
└── .github/
    └── FUNDING.yml      # GitHub sponsorship configuration
```

Naming convention: All lowercase with hyphens (e.g., wx-miniapp), Java package paths follow reverse domain naming (com.github.binarywang)
Layered structure: Standard Spring Boot layers including controller (API entry), config (configuration management), utils (utility classes), with global exception handling via error directory
Extension design: Supports containerized deployment via dedicated docker directory, frontend page separation via resources/templates, and Spring configuration extension via META-INF