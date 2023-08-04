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

### Spring

Spring重要特征是依赖注入，所有Spring模块不是依赖注入就是IOC控制反转，恰当的使用DI或者IOC，可以开发出高内聚低耦合的应用。

### SpringMVC

Spring MVC 提供了一种分离式的方法来开发 Web 应用。通过运用像 DispatcherServelet，MoudlAndView 和 ViewResolver 等一些简单的概念，开发
Web 应用将会变的非常简单。

### SpringBoot

Spring和SpringMVC的问题在于需要配置大量的参数，而SpringBoot通过一个自动装配和启动的项目来解决这个问题。同时为更好构建产品，SpringBoot提供了一些非功能性特性。

## 什么是Spring Boot Starter?

启动器是一套方便的依赖描述符，它可以放在自己的程序中。你可以一站式的获取你所需要的
Spring和相关技术，而不需要依赖描述符的通过示例代码搜索和复制黏贴的负载。例如，如果想使用Spring和JPA访问数据库，只需要项目包含`spring-boot-starter-data-jpa`
依赖性即可。

## 如何重新加载Spring Boot上的更改，而无需重新启动服务器？

SpringBoot有一个`DevTools`模块，可以提高开发人员生产力。开发人员可以重新加载SpringBoot的更改，而无须重新启动服务器。但该模块在应在生产环境中被禁用。

## RequestMapping 和 GetMapping 的不同之处在哪里？

`RequestMapping`是具有类属性的，可以进行`GET,POST,PUT`或者其他注释中具有的请求方法，`GetMapping`
是GET请求方法中的一个特例，它只是`RequestMapping`的一个延伸，目的是为了提高清晰度。

## SpringBoot的核心注解有哪些？

## SpringBoot读取配置文件有哪几种方式？

SpringBoot默认的配置文件有两种格式：`application.properties`和`application.yml`，查找顺序是首先从`application.properties`
查找；

- @PropertySource

  @PropertySource注解用于指定资源文件读取的位置，它不仅能读取properties文件，也能读取xml文
  件，并且通过YAML解析器，配合自定义PropertySourceFactory实现解析YAML文件

- @Value

  使用@Value读取配置文件，适用于对象参数比较少的情况；可以直接在对象属性上使用`@Value`注解,同时以`${}`
  形式传入配置文件中对应的属性，同时需要在该类上方使用`@Configuration`注解，将该类作为配置类

- @Environment

  Environment 是 SpringCore 中的一个用于读取配置文件的类，将此类使用 @Autowired 注入到类中就可以使用它的getProperty方法来获取某个配置项的值

- @ConfigurationProperties

  使用 @ConfigurationProperties 读取配置文件；如果对象的参数比较多情况下,推荐使用@ConfigurationProperties
  会更简单一些，不需要在每一个字段的上面的使用@Value注解。
  @ConfigurationProperties注解声明当前类为配置读取类prefix="rabbitmq" 表示读取前缀rabbitmq的属性

## SpringBoot如何定义多套不同环境配置

创建各环境对应的`yml`配置文件

```yaml
application.yml
application-dev.yml
application-test.yml
application-prod.yml
```

然后在`application.yml`文件中指定当前的环境`spring.profiles.active = test`,这时候读取的就是
application-test.yml文件。

## SpringBoot中如何实现定时任务

SpringBoot中对于定时任务的支持主要还是来自Spring框架。主要有两种方式：

- 使用Spring中的`@Scheduled`注解
- 使用第三方框架`Quartz`

使用Spring中的`@Scheduled`方式主要通过`@Scheduled`注解来实现；使用Quartz，定义`Job`和`Trigger`即可。

## SpringBoot的打成的jar和普通jar有什么区别？

Spring Boot项目最终打包成的jar是可执行jar，这种jar可以直接通过`java -jar xxx.jar`命令来运行，这种jar不可以作为普通的 jar
被其他项目依赖，即使依赖了也无法使用其中的类.

普通的jar包，解压后直接就是包（包中为代码），而SpringBoot打包成的可执行jar解压后，在/BOOT-INF/classes目录下才是代码，无法被直接引用，如果非要引用，可以在pom.xml文件中增加配置，将SpringBoot项目打包成两个jar，一个可执行，一个可引用。