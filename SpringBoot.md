## Import注解的三种使用方法

- 静态注入
- 实现了`ImportSelector`接口，并且实现了`selectImports`方法，那么返回值就是`selectImports`的方法的返回类型。
- 实现了`ImportBeanDefinitionRegister`接口，并且实现了`registerBeanDefinitions`方法，这时就可以自行封装`BeanDefinition`

## SpringBoot自动装配的核心配置文件有哪些？

```yml
META-INF/spring.factories              // 候选
META-INF/spring-autoconfigure-metadata.properties  // 过滤
```

## SpringBoot的自动装配流程是怎样的？

## bootstrap.yml文件的作用

SpringBoot默认支持的属性文件有如下四种：

- application.properties
- application.xml
- application.yml
- application.yaml

还有一类`bootstrap.yml，bootstrap.properties`。`bootstrap.yml`
在SpringBoot中默认不支持，需要在SpringCloud环境下才支持，其作用在于：SpringBoot项目启动之前启动一个父容器，该父容器可以在SpringBoot容器启动前完成一些加载初始化操作，比如加载配置中心中的信息等。

## SpringBoot如何解决跨域问题

- 跨域可以在前端通过JSONP解决，但是只支持`GET`方式请求
- SpringBoot中可以通过实现`WebMvcConfigurer`接口，重写其中的`addCorsMappings`方法，该方法中添加允许跨域的相关请求

```java
@Override
public void addCorsMappings(CoorsRegistry registry){
        registry.addMapping("/**")
        .allowOrigins("*")
        .allowCredentials(true)
        .allowedMethods("GET","POST","PUT","DELETE","OPTIONS")
        .maxAge(3600)
        }
```

## SpringBoot中如何配置log4j

SpringBoot项目中默认提供Logback日志框架，所以如果引入log4j，要先排除Logback的依赖，然后再添加log4j的依赖，然后在`src/main/resources`
目录下创建`log4j.properties`文件，然后就可以进行日志的相关配置。

## Spring Boot、 Spring MVC 和 Spring 有什么区别？

## 什么是Spring Boot Starter?

## 如何重新加载Spring Boot上的更改，而无需重新启动服务器？

## RequestMapping 和 GetMapping 的不同之处在哪里？

## SpringBoot的核心注解有哪些？

## SpringBoot读取配置文件有哪几种方式？

## SpringBoot如何定义多套不同环境配置

## SpringBoot中如何实现定时任务

## SpringBoot中的监视器是什么？

## SpringBoot的打成的jar和普通jar有什么区别？

##  