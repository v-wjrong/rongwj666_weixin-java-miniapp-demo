[Go to Homepage](../README.md)

## Project Overview
### Basic Project Information
- **Name:** spring-boot-demo-for-wechat-miniapp  
- **GroupId (Maven):** com.github.binarywang  
- **ArtifactId (Maven):** weixin-java-miniapp-demo  
- **Version:** 1.0.0-SNAPSHOT  
- **Primary Programming Language:** Java  

## Prerequisites  
- **JDK Version:** 1.8 (configured via Maven's `<maven.compiler.source>` and `<maven.compiler.target>` properties)  
- **Build Tool Version:** Maven (identified from `pom.xml` file)  
- **Network Middleware Dependencies:**  
  - Redis (inferred from `jedis` dependency but no explicit version specified)  

## Build Guide  
### Maven Build  
- Build Commands:  
    - Clean build: `mvn clean`  
    - Compile project: `mvn compile`  
    - Package project: `mvn package`  
    - Install to local repository: `mvn install`  
    - Deploy project: `mvn deploy`  
- Build Process:  
    - Maven's build process mainly includes phases such as clean, compile, test, package, verify, install, and deploy. This project uses Spring Boot and Docker plugins. After packaging, an executable JAR file is generated, and Docker images can be built via the Docker plugin.  
- Package Directory:  
    - The packaged JAR file is located in the `target/` directory with the filename `${project.build.finalName}.jar`. Docker-related files are in the `src/main/docker/` directory.  

## Dependency Management  
### Key Dependencies  
- **Spring Boot Web:** `spring-boot-starter-web` - Provides Spring MVC and embedded Tomcat support (version inherited from parent POM 2.6.3).  
- **Thymeleaf Template Engine:** `spring-boot-starter-thymeleaf` - Integrates Thymeleaf view technology (version inherited from parent POM).  
- **WeChat Mini Program SDK:** `weixin-java-miniapp` - WeChat Java Mini Program development toolkit (explicit version 4.7.0 managed via property `weixin-java-miniapp.version`).  
- **File Upload:** `commons-fileupload` - Apache Commons file upload component (explicit version 1.5).  
- **Test Support:** `spring-boot-starter-test` - Spring Boot test module (scope: test).  
- **Configuration Processing:** `spring-boot-configuration-processor` - Generates configuration metadata (marked as optional).  
- **Lombok:** `lombok` - Simplifies Java code (scope: provided).  
- **Redis Client:** `jedis` - Redis Java client (version inherited from parent POM or dependency management).  

### Adding/Modifying Dependencies  
- **Maven:** Add or modify `<dependency>` elements under the `<dependencies>` tag in the `pom.xml` file. For example:  
  ```xml
  <dependency>
      <groupId>org.example</groupId>
      <artifactId>new-dependency</artifactId>
      <version>1.0.0</version>
  </dependency>
  ```

### Dependency Version Management  
- **Maven (`<dependencyManagement>`):**  
  In this example, versions are primarily managed uniformly via the parent POM (`spring-boot-starter-parent`). For instance, versions of Spring Boot-related dependencies are derived from the parent POM's 2.6.3. Custom versions can be overridden via `<properties>` (e.g., `weixin-java-miniapp.version`) or by directly specifying `<version>`. To centralize version management, declare dependencies and their versions in `<dependencyManagement>`, eliminating the need for repeated version specifications in submodules.

## Project Structure

```text
weixin-java-miniapp-demo/
├── .editorconfig       # Editor configuration (standardized settings)
├── .gitignore         # Git ignore rules
├── README.md          # Project documentation
├── .travis.yml        # CI/CD configuration (Travis CI)
├── pom.xml            # Maven project configuration
├── commit.sh          # Git commit script (presumed)
├── src/
│   └── main/
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # SpringBoot main class
│       │       ├── controller/                # WeChat Mini Program controllers
│       │       │   ├── WxMaMediaController.java  # Media processing APIs
│       │       │   ├── WxMaUserController.java   # User-related APIs
│       │       │   └── WxPortalController.java   # Entry verification API
│       │       ├── utils/                     # Utility classes
│       │       │   └── JsonUtils.java         # JSON processing utility
│       │       ├── error/                     # Error handling
│       │       │   ├── ErrorController.java      # Error controller
│       │       │   └── ErrorPageConfiguration.java # Error page configuration
│       │       └── config/                    # WeChat configuration
│       │           ├── WxMaProperties.java    # Configuration properties class
│       │           ├── WxMaConfiguration.java # WeChat configuration class
│       │           └── ResourcesConfig.java   # Resource file configuration
│       ├── resources/
│       │   ├── application.yml.template       # Application configuration template
│       │   ├── templates/                    # Frontend templates
│       │   │   └── error.html                # Error page template
│       │   └── META-INF/                     # Metadata configuration
│       │       └── additional-spring-configuration-metadata.json  # Spring configuration metadata
│       └── docker/
│           └── Dockerfile                    # Container deployment configuration
└── .git/               # Git version control directory (standard VCS structure)

Naming convention: Standard Java package naming (com.github.* reverse domain) with camelCase class names
Layered structure: Standard SpringBoot layers including config/controller/utils, with dedicated WeChat Mini Program configuration layer
Extension design: Containerization support via standalone docker directory, resources/META-INF providing Spring configuration extension capability
```