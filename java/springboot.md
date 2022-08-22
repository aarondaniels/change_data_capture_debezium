# Spring Boot

Spring is an application framework for Java. Spring Boot takes Spring and makes it easy to create stand-alone Spring applications. 

This will be an exercise in creating an application from [Spring Boot](https://spring.io/projects/spring-boot)

1. Navigate to [Spring Boot](https://start.spring.io) to start the application. Leave the default parameters and, from the dependencies section, add Spring Web to create a web server. Select 'Generate' to download the demo.zip file to the local machine
2. Create the container with, `docker run -it --rm -p 8080:8080 --name javamaven maven:3.6.3-openjdk-11 bash` and then add an editor inside the container (recall, `apt-get update` and `apt-get install vim nano`)
3. Copy files, unzipped, from #1 into the home directory of the javamaven container created in #2
4. Modify code using the nano editor by first accessing the demo application, DemoApplication.java (in this case, the file is located /home/src/main/java/com/example/demo). Remove default code and replace with the following:
``` java 
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class DemoApplication {

    public static void main(String[] args) 
    {
    SpringApplication.run(DemoApplication.class, args);
    }

    @GetMapping("/hello")
    public String hello(@RequestParam(value = "name", defaultValue="World") String name)
    {
        return String. format("Hello %s!", name);
    }
}
```
Save the file and confirm the code update was successful with the following command, `cat demoApplication.java`
5. Run the application, `mvn spring-boot:run` from the root of the application (in this case, /home)
6. Access the app from the host machine. Go to the browser and search for it in the designated browser at localhost:8080/hello, which would display, "Hello, world." A value can be passed in through the URL to modify this. For example, if the URL was changed to `localhost:8080/hello?name=Peter` would yield, "Hello Peter!"



