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
- **Build Tool Version:** Maven (identified from the `pom.xml` file; no explicit Maven version specified; recommended to use a version compatible with Spring Boot 2.6.3)  
- **Network Middleware Dependencies:**  
  - Redis (inferred from the `jedis` dependency; no explicit version specified)  

## Build Guide  
### Maven Build  
- Build Commands:  
    - Clean build: `mvn clean`  
    - Compile project: `mvn compile`  
    - Package project: `mvn package`  
    - Install to local repository: `mvn install`  
    - Deploy project: `mvn deploy`  
- Build Process:  
    The Maven build process mainly includes the following phases:  
    1. **Clean (clean):** Deletes the `target` directory and generated build files.  
    2. **Compile (compile):** Compiles the project's source code.  
    3. **Test (test):** Executes unit tests.  
    4. **Package (package):** Packages the compiled code into a JAR or WAR file.  
    5. **Verify (verify):** Checks the packaged results to ensure quality.  
    6. **Install (install):** Installs the packaged file into the local Maven repository.  
    7. **Deploy (deploy):** Deploys the packaged file to a remote Maven repository.  
- Output Directory:  
    - The packaged file (e.g., JAR or WAR) is generated in the `target/` directory.  
    - Example: `target/weixin-java-miniapp-demo-1.0.0-SNAPSHOT.jar`.  
    - If the Docker plugin is used, Docker-related files are placed in the `src/main/docker/` directory.  

## Dependency Management  
### Key Dependencies  
- **Spring Boot Web:** `spring-boot-starter-web` - Provides Spring MVC and embedded Tomcat support (version inherited from parent POM 2.6.3).  
- **Thymeleaf:** `spring-boot-starter-thymeleaf` - Template engine support (version inherited from parent POM).  
- **WeChat Mini Program SDK:** `weixin-java-miniapp:4.7.0` - WeChat Mini Program Java SDK (managed via the `weixin-java-miniapp.version` property).  
- **File Upload:** `commons-fileupload:1.5` - Apache Commons file upload component.  
- **Testing:** `spring-boot-starter-test` - Spring Boot testing support (scope: test).  
- **Lombok:** `lombok` - Annotation-driven code generation tool (scope: provided).  
- **Redis Client:** `jedis` - Redis Java client (version inherited from parent POM).  

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
  This POM centrally manages most dependency versions through the parent POM (`spring-boot-starter-parent:2.6.3`). Custom versions can be overridden via `<properties>` (e.g., `weixin-java-miniapp.version`) or by directly specifying `<version>`. To uniformly manage submodule dependencies, use `<dependencyManagement>` in the parent POM to define versions without introducing dependencies.

## Project Structure

```text
weixin-java-miniapp-demo/
├── .editorconfig       # Editor configuration (standardized settings)
├── .gitignore         # Git ignore rules
├── README.md          # Project documentation
├── .travis.yml        # CI/CD configuration (Travis CI)
├── pom.xml            # Maven project configuration file
├── commit.sh          # Git commit script (inferred)
├── src/
│   └── main/
│       ├── resources/
│       │   ├── application.yml.template  # Spring Boot configuration template
│       │   ├── tmp.png                   # Temporary image resource (inferred)
│       │   ├── templates/
│       │   │   └── error.html           # Error page template
│       │   └── META-INF/
│       │       └── additional-spring-configuration-metadata.json  # Spring configuration metadata
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # Spring Boot main class
│       │       ├── controller/               # WeChat Mini Program controllers
│       │       │   ├── WxMaMediaController.java   # Media processing controller
│       │       │   ├── WxMaUserController.java    # User management controller
│       │       │   └── WxPortalController.java    # Entry controller
│       │       ├── utils/                    # Utility classes
│       │       │   └── JsonUtils.java        # JSON processing utility
│       │       ├── error/                    # Error handling module
│       │       │   ├── ErrorController.java      # Global error controller
│       │       │   └── ErrorPageConfiguration.java  # Error page configuration
│       │       └── config/                   # WeChat configuration module
│       │           ├── WxMaProperties.java       # WeChat configuration properties
│       │           └── WxMaConfiguration.java    # WeChat configuration class
│       └── docker/
│           └── Dockerfile                # Container deployment configuration
├── .git/                                # Git version control directory (standard VCS structure)
└── .github/                             # GitHub platform configuration
    └── FUNDING.yml                      # GitHub sponsorship configuration
```

Naming conventions: Follows Java standard package naming (com.github.organization), directories use lowercase kebab-case (e.g., miniapp-demo)

Layered architecture:
1. Controller layer: Handles WeChat API requests
2. Configuration layer: Manages WeChat SDK configurations
3. Utility layer: Provides JSON serialization capabilities
4. Error handling layer: Implements global exception interception
5. Resource layer: Contains static templates and configurations

Extension design:
1. Supports containerized deployment via dedicated docker directory
2. Configuration template (application.yml.template) enables environment isolation
3. .travis.yml provides CI extension points
4. META-INF supports Spring Boot configuration extensions