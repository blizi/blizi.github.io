---
layout: post
title: "springboot笔记"
date: 2019-04-16 22:53:06 
description: "springboot"
tag: springboot
---

```java
@Controller
public class Hello {
    @GetMapping(value = "/hello")
    @ResponseBody
    public String hello(){
        return "desire";
    }
}
```

#### @Controller  @ResponseBody可用 @RestController代替  如下：

```java
@RestController
public class Hello {
    
    @GetMapping(value = "/hello")
    public String hello(){
        return "desire";
    }
}
```

#### 参数传递

##### @PathVariable("")

```java
@RestController
public class Hello {
    
    @GetMapping(value = "/hello/{name}")
    public String hello(@PathVariable("name") String data){
        return data+"'s desire";
    }
}
```

##### @RequestParam(value = "",defaultValue = "",required=false)

```java
@RestController
public class Hello {
    @GetMapping(value = "/hello")
    public String hello(@RequestParam("name") String data){ // 传递的参数名为name
        return data+"'s desire";
    }
}
defaultValue   //  默认参数
required = false //   参数是否为必须的
```

##### @requestbody

```java
  @PostMapping(value = "/hello")
    public User hello(@RequestBody User user){
        return user;
    }
```

##### 多个url对应一个

```java
 @GetMapping(value = {"/hello/{name}","hi/{name}"})
    public String hello(@PathVariable("name")String name){
        return name;
    }
```

#### pom.xml

```xml
<properties>
        <java.version>1.8</java.version>
    </properties>

    <!--spring boot的父组件-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.4.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <!--添加依赖-->
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

    <!--添加Maven插件-->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

##### 启动类

```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}
```

##### jar包启动

```java
用maven工具lifecycle下的package打包后在终端执行：
java -jar xxxx.jar
```

#### Swagger

###### pom.xml

```xml
 <dependency>
     <groupId>io.springfox</groupId>
     <artifactId>springfox-swagger2</artifactId>
     <version>2.9.2</version>
 </dependency>

 <dependency>
     <groupId>io.springfox</groupId>
     <artifactId>springfox-swagger-ui</artifactId>
     <version>2.9.2</version>
 </dependency>
```



#### 配置文件

```properties
//修改端口
server.port=8081  
//项目路径
server.servlet.context-path=/first_demo
```

##### 多套配置文件的选择

​	现有application-dev.properties和application-pro.properties两套配置文件，在application.properties中选择激活哪一份配置文件

```properties
spring.profiles.active=dev      // 使用application-dev.properties文件
spring.profiles.active=pro      //使用application-pro.properties文件
```

#### 配置文件参数绑定属性



> @Value("")  // 注解  单个绑定
>
> ${xx.xxx}    //方式

```properties
person.name = 张三
person.age = 16
person.info = man
```

```java
    @Value("${person.name}")
    private String name;
    @Value("${person.age}")
    private String age;
    @Value("${person.info}")
    private String info;
```

> ```java
> @ConfigurationProperties("person") //批量绑定   person中的属性容器中的属性才可以使用此注解,支持松散语法(驼峰命名)
> @Component   //加入spring容器
> ```

> lomlok 
>
> @Data   //免去getter/setter，tostring()





<br>

转载请注明：[blizi的博客](blizi.club) » 