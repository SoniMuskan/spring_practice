# spring_practice
If you don't have Spring Initializr integrated in IntelliJ IDEA, you can still create a Spring Boot project manually by following these steps:

### 1. Install IntelliJ IDEA and JDK
Ensure you have IntelliJ IDEA and JDK installed as mentioned before.

### 2. Create a New Maven Project
1. Open IntelliJ IDEA.
2. Click on `File > New > Project`.
3. Select `Maven` from the list and click `Next`.
4. Fill in the necessary details:
   - GroupId: `com.example`
   - ArtifactId: `demo`
   - Version: `1.0-SNAPSHOT`
   - Name: `demo`
   - Description: `Demo project for Spring Boot`
   - Package: `com.example.demo`
5. Click `Next`, then `Finish`.

### 3. Add Spring Boot Dependencies
1. Open the `pom.xml` file in your project root directory.
2. Add the Spring Boot parent POM and dependencies as follows:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <name>demo</name>
    <description>Demo project for Spring Boot</description>
    <packaging>jar</packaging>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.4</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

### 4. Create the Main Application Class
1. In the `src/main/java/com/example/demo` directory, create a file named `DemoApplication.java`.
2. Add the following code to `DemoApplication.java`:

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @RestController
    class HelloController {
        @GetMapping("/")
        public String hello() {
            return "Hello, World!";
        }
    }
}
```

### 5. Run the Application
1. Right-click on the `DemoApplication.java` file.
2. Select `Run 'DemoApplication'`.

### 6. Test the Application
Open your web browser and navigate to `http://localhost:8080`. You should see `Hello, World!`.

### Summary
You have created a Spring Boot project manually by setting up a Maven project, adding the necessary Spring Boot dependencies, creating a main application class, and running the application. This approach works even if you don't have the Spring Initializr integrated with your IntelliJ IDEA.
