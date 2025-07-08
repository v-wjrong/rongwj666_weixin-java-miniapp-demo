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
- **Build Tool Version:** Maven (identified from the `pom.xml` file; recommended version compatible with Spring Boot 2.6.3, typically 3.6.3+)  
- **Network Middleware Dependencies:**  
  - Redis (inferred from the `jedis` dependency, but no explicit version is specified, managed by Spring Boot parent POM)  
  - WeChat Mini Program SDK (`weixin-java-miniapp`, version 4.7.0)  

## Build Guide  
### Maven Build  
- Build Commands:  
    - Clean build: `mvn clean`  
    - Compile project: `mvn compile`  
    - Package project: `mvn package`  
    - Install to local repository: `mvn install`  
    - Deploy project: `mvn deploy`  
- Build Process:  
    - Maven's build process mainly includes the following phases: clean, compile, test, package, verify, install, and deploy. This project uses the Spring Boot Maven plugin, which generates an executable JAR file after packaging.  
- Packaging Directory:  
    - The packaged JAR file is located in the `target/` directory, named `${project.build.finalName}.jar` (e.g., `weixin-java-miniapp-demo-1.0.0-SNAPSHOT.jar`).  
    - For Docker image builds, the related configuration files are in the `src/main/docker/` directory. The built image name is `${docker.image.prefix}/${project.artifactId}` (e.g., `wx-miniapp-demo/weixin-java-miniapp-demo`).  

## Dependency Management  
### Key Dependencies  
- **Spring Boot Core Support**  
  - `spring-boot-starter-web` (Web development support)  
  - `spring-boot-starter-thymeleaf` (Template engine)  
  - `spring-boot-starter-test` (Test support, scope=test)  
  - `spring-boot-configuration-processor` (Configuration metadata generation, optional=true)  
  - Version inherited from the parent project `spring-boot-starter-parent:2.6.3`  

- **WeChat Mini Program SDK**  
  - `weixin-java-miniapp:4.7.0` (version managed via property `${weixin-java-miniapp.version}`)  

- **Utility Libraries**  
  - `commons-fileupload:1.5` (File upload)  
  - `lombok` (Code simplification, scope=provided)  
  - `jedis` (Redis client, version inherited from the parent project)  

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
  The current project manages most dependency versions uniformly through the parent POM (`spring-boot-starter-parent`), e.g., Spring Boot component versions are `2.6.3`. Custom dependency versions can be defined via `<properties>` (e.g., `${weixin-java-miniapp.version}`) or directly specified in `<dependency>`.

## Project Structure

```text
weixin-java-miniapp-demo/
├── .editorconfig       # Editor configuration (standardized settings)
├── .gitignore         # Git ignore rules
├── README.md          # Project documentation
├── .travis.yml        # CI/CD configuration (Travis CI)
├── pom.xml            # Maven project configuration file
├── commit.sh          # Git commit script (presumed)
├── src/
│   └── main/
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # SpringBoot main class
│       │       ├── controller/               # WeChat Mini Program controllers
│       │       │   ├── WxMaMediaController.java  # Media processing APIs
│       │       │   ├── WxMaUserController.java    # User-related APIs
│       │       │   └── WxPortalController.java    # WeChat message entry
│       │       ├── utils/                    # Utility classes
│       │       │   └── JsonUtils.java        # JSON processing utility
│       │       ├── error/                   # Error handling
│       │       │   ├── ErrorController.java  # Global exception handler
│       │       │   └── ErrorPageConfiguration.java # Error page configuration
│       │       └── config/                   # WeChat configuration
│       │           ├── WxMaProperties.java   # Configuration properties class
│       │           └── WxMaConfiguration.java # WeChat configuration class
│       ├── resources/
│       │   ├── application.yml.template      # Configuration template
│       │   ├── templates/                    # Frontend templates
│       │   │   └── error.html                # Error page template
│       │   └── META-INF/                     # Metadata configuration
│       │       └── additional-spring-configuration-metadata.json  # Spring configuration extension
│       └── docker/
│           └── Dockerfile                    # Containerization deployment configuration
└── .git/                # Git version control directory (standard VCS structure)
```

Naming convention: Follows Java standard package naming (com.github.organization), directories use lowercase hyphenated style  
Layered structure: Typical SpringBoot layers including controller/config/utils, with dedicated WeChat Mini Program configuration layer  
Extension design: Supports containerization via standalone docker directory, META-INF provides Spring configuration extension capability