# Spring 

## Loose Coupling vs Tight Coupling

Loosing coupling enables the system components to work independently. It provides maintainability, extensibility, scalability and makes the entire framework more stable. In this scenario, it makes possible to modify code without shuttering it. It reduces the dependency between components and decreases the risk of breaking changes.

In Tight coupling, in other hand, classes are dependent on each other. It has dependency hard coded declared inside the method. Tight coupling only uses only one device, one interface and one API. It is ideal for small applications because it makes it easier to identify changes. It is designed for singular workflow purposes.

### Tight Coupling

Imagine that as part of a complex algorithm it is necessary sort some data. In a tight coupling scenario, an instance of BubbleSortAlgorithm is created inside the ComplexAlgorithm class. As a result, the class depends on the instance of BubbleSortAlgorithm to work properly. If someday someone decide change the sorting algorithm, you'll have to change the implementation of the class.

```java

public class ComplexAlgorithm {
  BubbleSortAlgorithm bubbleSortAlgotithm = new BubbleSortAlgorithm();
}

``` 

### Loose Coupling

In this example, we have an interface called SortAlgorithm that owns a method, called sort. There are two implementations for sort (QuickSortAlgorith and BubbleSortAlgorithm). This way, ComplexAlgorithm makes use of SortAlgorithm. @Autowired provides a constructor that can create an instance of one of two implementations of SortAlgorithm and pass it to Complex Algorithm.


```java

@Component
public class ComplexAlgorithm {
  @Autowired
  private SortAlgorithm sortAlgorithm;
}

``` 

```java

public interface SortAlgorithm {
  public int[] sort(int[] numbers);
}

``` 

```java

public class QuickSortAlgorith implements SortAlgorithm {

``` 

```java

public class BubbleSortAlgorithm implements SortAlgorithm {

``` 

## Dependencies

Whenever a class A uses another class or interface B, then A depends on B. A cannot carry out its work without B, and A cannot be reused without also reusing B. In such a situation the class A is called the "dependant" and the class or interface B is called the "dependency". A dependant depends on its dependencies.

[Dependencies](https://jenkov.com/tutorials/ood/understanding-dependencies.html)


## Dependency Injection 

Dependency injection is a programming technique that makes a class independent of its dependencies. It achieves that by decoupling the usage of an object from its creation. 

### Autowired

 (@Autowired) is an anotation used for dependency injection. It indicates where the dependency should be injected. It works on methods, constructors and attributes. It can only be used once per constructor

## Inversion of control

Inversion of control is a software design principle that asserts a program can benefit in terms of pluggability, testability, usability and loose coupling if the management of an application's flow is transferred to a different part of the application.

### Important Roles of an IOC Container

The three essential roles of an IOC Container are _finding beans_, _wire dependencies_ and _manage beans' life cycle_

Application Context can be created using @Configuration anotation. Along side the basic roles of an IOC Container, it provides Spring AOP features, I18n capabilities, WebApplicationContext for web application. If you want to save memory, instead of using Application Context, you can use _Bean Factory_, the simplest tool Spring provides. It enables you to use only all three essential roles of an IOC Container. 

```java
@Configuration
class SpringCOntext {
}

ApplicationContext = context =
 new AnnotationConfigApplicationContext(SpringContext.class);
);
``` 

The other way of adding Application Context is using XML. To create an application context, you can use ClassPathXmlApplicationContext

```java
ApplicationContext = context =
 new ClassPathXmlApplicationContext(
 new String[] {"BusinessApplicationContext.xml", "Other-Configuration.xml"}
);
``` 
We can also create Application Contextss on Unit Tests using SpringJUnit4ClassRunner


```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = JavaTestContext.class)
public class DependencyInjectionJavaContextRxamples {
``` 

## Main features Spring

- Dependency Injection
- Resolves Duplication/Plumbing Code
- Good Integration with Other Frameworks

# Spring MVC

Provides decoupled way of developing web applications.
Dispatcher Servlet
ModelAndView
ViewResolver

# Spring Boot

- Eliminates all configuration needed by Spring and Spring MVC and auto configures it
	- No need for @ComponentScan.
	- No need to configure DispatcherServlet, Data Source, Entity Manager Factory ot Transaction Manager

## Auto Configuration
	
Based on frameworks available on CLASSPATH and existing configuration on the application, Spring Boot provides the application with the basic configuration necessary. It's implemented on spring-boot-autoconfigure.jar. It holds all configuration for the Spring project to run.
To get more details, turn on Debug logging or use Spring Boot Actuator

## @SpringBootAplication

On the top of all spring boot class should be an @SpringBootAplication anotation 

This anotation provides @SpringBootConfiguration, @EnableAutoConfiguration and @ComponentScan

## Embedded Servers

In order to run a web application, before Spring Boot, it was necessary install a server, such as TomCat, on the deployment environment before start programming. Spring Boot provides an Embedded Server, which means that the server is embedded as part of the deployable jar. The default embedded server in Spring Boot is TomCat. It also supports Jetty and UnderTow.

# Starter Projects

Starters are a set of convenient dependency descriptors that you can include in your application. You get an one-stop-shop for all the Spring and related technology that you need, without having to hunt through sample code and copy and paste loads of dependency descriptors.

**spring-boot-starter-web-services**: SOAP web services
**spring-boot-starter-web**: web and RESTful applications
**spring-boot-starter-test** Unit, Integration testing (included by default)
**spring-boot-starter-jdbc**: traditional JDBC
**spring-boot-starter-hateoas**: HATEOAS features
**spring-boot-starter-security**: Authentication and Authorization using Spring Security
**spring-boot-starter-data-jpa**: Spring Data JPA with Hibernate
**spring-boot-starter-cache**: Enable spring framework caching support
**spring-boot-starter-data-rest**: Expose simple REST services using spring data REST

# Starter Parents

Defines dependency versioning on the project

# Spring Initializr

It is a tool for bootstrapping Spring Boot projects ![Spring Initializr/](https://start.spring.io/)

# Application Properties

Used to configure Spring Boot Applications ![Application Properts](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)


# Profiles

Tool for configurating different envoronments. Uses Application.Properties to set every environment. 
Based on the active profile, appropriate configuration is picked up
Used to configure resources - databases, queues, external services


# Spring Boot Actuator

Use for monitoring application

- env/ metrics / trace/ dump
- beans / autoconfig / configprops / mappings

URL has changed in Spring Boot 2.0 to /application

Just by adding spring-boot-starter-actuator dependency, the app starts being monitored


# Command Line Runner

spring documentation - interface used to indicate that a bean should run when it is contained within a Spring Application

# Maven x Graddle

[Comparison](https://www.geeksforgeeks.org/difference-between-gradle-and-maven/)

# @ConfigurationProperties


[ARTICLE](https://www.baeldung.com/configuration-properties-in-spring-boot)

# @Bean

[ARTICLE](https://www.devmedia.com.br/introducao-aos-javabeans/8621)

## Component Scan

Spring searches for components that we use. In order to inform Spring where it can find those components, in Java COnfiguration it`s necessary to set component scan like this:

```java
@Configuration
@ComponentScan(basePackages = {
  "com.in28minutes.spring.example1.businessservice",
  "com.in28minutes.spring.example1.dataservice.stup" 
})
```
You can also configure it using XML

# @Component vs @Autowired

- *@Component* - Spring should manage the bean.
- *@Autowired* - Spring should find the matching bean and wire the dependency in.

# @Component vs @Autowired vs @Service vs @Controller

- *@Component* - Generic component. (web layer)
- *@Repository* - encapsulating storage, retrieval, and search behaviour typically from a relational database (data layer)
- *@Service* - Business Service Facade (business layer)
- *@controller - Controller in MVC pattern

# Bean Scopes

- *singleton* - One instance per Spring Context. That's the default scope on Spring
- *prototype* - new bean whenever requested
- *request* - One bean per HTTP request. Web-aware Spring ApplicationContext.
- *session* - one bean per HTTP session. Web-aware Spring ApplicationContext.

Beans are not thread safe by default because if on a singleton there is one bean for all threads running.
Gang of Four design pattern defines Singleton as having one instance per ClassLoader. However, Spring singleton is defined as one instance of bean definition per container.

