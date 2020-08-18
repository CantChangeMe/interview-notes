

## 1. What is Spring Boot?
Spring Boot is basically an extension of the Spring framework which eliminated the boilerplate configurations required for setting up a Spring application. Spring Boot is designed to reduce boiler plate configuration providing you the shortest way to have a Spring web application up and running as quickly as possible, with minimal upfront configuration

## 2. What are the features of Spring Boot
As per Spring Boot website, it has following features:

* Create **stand-alone Spring applications**
* **Embed Tomcat, Jetty or Undertow** directly (no need to deploy WAR files)
* Provide **opinionated 'starter' dependencies** to simplify your build configuration
* **Automatically configure Spring and 3rd party libraries** whenever possible
* Provide **production-ready features such as metrics, health checks** 

## 3. What are the limitations of Spring Boot
* You need to keep control on your app dependencies otherwise, it may unnecessarily increase the deployment binary size with unused dependencies.
* It is time consuming process to migrate existing Spring Framework projects into Spring Boot.

## 4. Embedded Web Servers
* For servlet stack applications, the spring-boot-starter-web **includes Tomcat by including spring-boot-starter-tomcat, but you can use spring-boot-starter-jetty or spring-boot-starter-undertow** instead.

* For reactive stack applications, the spring-boot-starter-webflux includes **Reactor Netty by including spring-boot-starter-reactor-netty, but you can use spring-boot-starter-tomcat, spring-boot-starter-jetty, or spring-boot-starter-undertow** instead

## 5. What is the default embedded server with Spring Boot?
Tomcat is default embedded server with Spring Boot which comes with spring-boot-starter-web as part of its dependency. Use Jetty instead of default Tomcat:
```
<properties>
	<servlet-api.version>3.1.0</servlet-api.version>
</properties>
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
	<exclusions>
		<!-- Exclude the Tomcat dependency -->
		<exclusion>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
		</exclusion>
	</exclusions>
</dependency>
<!-- Use Jetty instead -->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```

## 6. How to disable Embedded Web Servers
Add following line in application.properties spring.main.web-application-type=none

## 7. What are Spring Boot Starters?
Starters are a set of convenient dependency descriptors that you can include in an application. For example, if you want to get started using Spring and JPA for database access, you won't need to hunt through sample code and copy-paste loads of dependency descriptors. You can just include the spring-boot-starter-data-jpa dependency in your project.

## 8. Explain commonly used Spring Boot Annotations
**@EnableAutoConfiguration** - EnableAutoConfiguration attempts to automatically configure the Spring Application Context and beans that you are likely to need.. For example: If you have SQLDB on your classpath, and you have not manually configured any database connection beans, then Spring Boot auto-configures an in-memory database.

**@ComponentScan** - It is used to specify the base packages to scan. It tells Spring that which packages should be managed by Spring. If you have a class annotated with @Controller which is in a package which is not scanned by Spring, you will not be able to use it as Spring controller. Even classes annotated with @Configuration are candidates for component scanning as @Configuration annotation is meta-annotated with @Component. Example :
```Java
@ComponentScan({"com.my.package.first","com.my.package.second"})
public class AppConfig 
or you can use type-safe alternative to specifying a base-package location as a String
```
```Java
@ComponentScan(basePackageClasses = {ExampleController.class, ExampleModel.class})
public class AppConfig
```
**@Bean** - It tells Spring that a method produces a bean and that needs to be managed by the Spring container. By default, the bean name will be the same as the method name. It is a method-level annotation.
Singleton scope is the default scope for a bean. It can be overridden by supplying the scope attribute to @Bean annotation

```Java
@Configuration
public class AppConfig {
    @Bean
    public NetworkService networkService() {
        return new NetworkServiceImpl();
    }
    @Bean(scope=DefaultScopes.PROTOTYPE)
    public Encryptor encryptor() {
        // ...
    }
}
```

You can customize bean name. Check the example here

**@Component** - It is used to indicate a class as a bean so at the time of component scanning, spring can auto-detect and auto-configure beans using classpath scanning. There’s an implicit one-to-one mapping between the annotated class and the bean (i.e. one bean per class). By default, the bean instance of this class has the same name as the class name with a lowercase initial. We can specify a different name using the optional value argument of this annotation. It is a class level annotation.

**@Repository** - It is a specialization of @Component . It indicates DAO component or Repository classes which represent the database access or persistence layer in an application.

**@Controller** - It is also a specialization of @Component. It indicates that this class serves as a controller component in the presentation layer. When we add the @Controller annotation to a class, we can use another annotation i.e. @RequestMapping - to map URLs to instance methods of a class. We can use @RequestMapping in only those methods whose classes are annotated with @Controller and it will NOT work with @Component, @Service, @Repository etc.

**@Service** - It is also a specialization of @Component. The classes with business logic are annotated with this annotations and call methods in the repository layer.

**@RestController** - This annotation is a specialized version of @Controller which itself is annotated with @Controller and @ResponseBody. So it automatically adds @Controller and @ResponseBody annotation automatically. So we do not have to add @ResponseBody to our request mapping methods. Read more

**@Configuration** - It indicates that a class declares one or more @Bean methods and may be processed by the Spring container to generate bean definitions and service requests for those beans at runtime. It's a replacement to the XML based configuration for configuring spring beans. Example:

```Java
@Configuration
 public class AppConfig {
     @Bean
     public MyBean1 myBean1() {
         // instantiate, configure and return bean
     }
     @Bean
     public MyBean2 myBean2() {
         // instantiate, configure and return bean
     }
 }
```

**@SpringBootApplication** : It includes following annotations:

 * @EnableAutoConfiguration
 * @ComponentScan
 * @Configuration

**@Autowired** - It is used for automatic injection of beans on the setter method, constructor or a field.

**@Qualifier** - By default, Spring resolves entries for injection by its type. If there are more than one beans of the same type in the spring container, it will throw NoUniqueBeanDefinitionException.@Qualifier annotation is used to eliminate the issue of which bean needs to be injected.

```Java
@Service("vehicleService")
public class VehicleCustomService implements CustomService {
   // class implimentation
}

@Service("applianceService")
public class ApplianceCustomService implements CustomService {
   // class implimentation
}

@Component
public class DemoService {
    @Autowired
    @Qualifier("vehicleService")
    private CustomService customService;
}
```

## 1. How to make spring frameworks log level to DEBUG
  
  logging.level.org.springframework = DUBUG

## 2. What steps spring framework follows when you start the application?
<pre>
  1.It does component scan for all the beans annotated with @Component,@Respository,@Service etc.
  2.It creates beans for them.
  3.It creates beans for dependencies also and autowires them and autovires them.
 <pre>

## 3. Setter or Constructor injection
  For injecting mandatory dependencies we use constrcutor injection.For optional dependencies we can use setter injection.
  
## 4. Do we really need to use @Autowired for setter or constructor? Or even do we need setter or constructor.
    No .We dont need @Autowired annotation on setters or contructor.We dont even need setter or constructor.
    Just use member variable with @Autowired annotaion.
  
