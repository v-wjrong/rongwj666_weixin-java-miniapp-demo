[Go to Homepage](../README.md)

## Project Overview  
### Basic Project Information  
- **Name:** spring-boot-demo-for-wechat-miniapp  
- **GroupId (Maven):** com.github.binarywang  
- **ArtifactId (Maven):** weixin-java-miniapp-demo  
- **Version:** 1.0.0-SNAPSHOT  
- **Primary Programming Language:** Java  

## Prerequisites  
- **JDK Version:** 1.8 (based on Maven's `<maven.compiler.source>` and `<maven.compiler.target>` properties)  
- **Build Tool Version:** Maven (identified from the `pom.xml` file)  
- **Network Middleware Dependencies:**  
  - Redis (inferred from the `jedis` dependency, but no explicit version specified)  

## Build Guide  
### Maven Build  
- Build Commands:  
    - Clean build: `mvn clean`  
    - Compile project: `mvn compile`  
    - Package project: `mvn package`  
    - Install to local repository: `mvn install`  
    - Deploy project: `mvn deploy`  
- Build Process:  
    - Maven's build process mainly includes phases such as clean, compile, test, package, verify, install, and deploy. This project uses Spring Boot and Docker plugins. After packaging, an executable JAR file will be generated, and Docker image building is supported.  
- Output Directory:  
    - The packaged JAR file is located in the `target/` directory, named `${project.build.finalName}.jar` (e.g., `weixin-java-miniapp-demo-1.0.0-SNAPSHOT.jar`).  
    - If using the Docker plugin to build the image, Docker-related files should be placed in the `src/main/docker/` directory. The built image name is `${docker.image.prefix}/${project.artifactId}` (e.g., `wx-miniapp-demo/weixin-java-miniapp-demo`).  

## Dependency Management  
### Main Dependencies  
- **Spring Boot Core Dependencies:**  
  - `spring-boot-starter-web`: Web application support (version inherited from parent POM 2.6.3)  
  - `spring-boot-starter-thymeleaf`: Thymeleaf template engine integration  
  - `spring-boot-starter-test`: Test support (scope=test)  
  - `spring-boot-configuration-processor`: Configuration metadata generation (optional=true)  

- **WeChat Mini Program SDK:**  
  - `weixin-java-miniapp`: WeChat Mini Program Java SDK (version managed by property `${weixin-java-miniapp.version}`, currently 4.7.0)  

- **Utility Libraries:**  
  - `commons-fileupload`: File upload functionality (explicitly specified version 1.5)  
  - `lombok`: Code simplification tool (scope=provided)  
  - `jedis`: Redis client (version inherited from parent POM)  

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
  1. Most Spring Boot-related dependency versions are uniformly managed via the parent POM (`spring-boot-starter-parent`).  
  2. Custom properties manage specific dependency versions (e.g., `<weixin-java-miniapp.version>4.7.0</weixin-java-miniapp.version>`).  
  3. Explicitly declaring the `<version>` tag overrides inherited versions (e.g., `commons-fileupload`).  
  4. If no version is specified, versions are automatically inherited from the parent POM or dependency management section.

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
│       │   ├── tmp.png                   # Temporary image resource (presumed)
│       │   ├── templates/
│       │   │   └── error.html           # Error page template
│       │   └── META-INF/
│       │       └── additional-spring-configuration-metadata.json  # Spring configuration metadata
│       ├── java/
│       │   └── com/github/binarywang/demo/wx/miniapp/
│       │       ├── WxMaDemoApplication.java  # Spring Boot main class
│       │       ├── controller/
│       │       │   ├── WxMaMediaController.java  # WeChat media API controller
│       │       │   ├── WxMaUserController.java   # WeChat user API controller
│       │       │   └── WxPortalController.java   # WeChat entry controller
│       │       ├── utils/
│       │       │   └── JsonUtils.java      # JSON utility class
│       │       ├── error/
│       │       │   ├── ErrorController.java       # Error handling controller
│       │       │   └── ErrorPageConfiguration.java  # Error page configuration
│       │       └── config/
│       │           ├── WxMaProperties.java    # WeChat Mini Program configuration properties
│       │           └── WxMaConfiguration.java # WeChat Mini Program configuration class
│       └── docker/
│           └── Dockerfile  # Container deployment configuration
└── .github/
    └── FUNDING.yml         # GitHub sponsorship configuration
```

Naming convention: Standard Java package naming (com.github.organization.project), directories use lowercase kebab-case (e.g., miniapp)

Layered structure:
1. Controller layer: `controller` package handles WeChat API requests
2. Utility layer: `utils` package provides JSON serialization capabilities
3. Configuration layer: `config` package manages WeChat SDK settings
4. Error handling: Dedicated `error` package for global exception handling
5. Resource layer: `resources` directory contains static assets and templates

Extension design:
1. Containerization support via dedicated `docker` directory
2. Configuration template mechanism (application.yml.template)
3. Comprehensive error handling system (error controller + page template)
4. CI/CD integration (.travis.yml)
5. Standardized Spring configuration metadata (META-INF)
```