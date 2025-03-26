2025-01-28 21:47

Status: [[Spring Boot]]

Tags: [[complete]]


# Introduction To Spring



## What is Servlet && Servlet Containers: 
Provides foundation for building we apps.
Servlet is java class which handles client request, process it ad return the response.
Servlet container are the ones which manages the servlets.
```txt
	    +------------------------------------------------+
        |                Service Container              |
        |                (Tomcat Server)                |
        |  (Our application is deployed here)           |
        +------------------------------------------------+
                          │
                          │ Input Request
                          ▼
        +------------------------------------------------+
        |                 Web.xml                        |
        |          (Servlet Mapping)                     |
        +------------------------------------------------+
                          │
       (1) Determines which Servlet to invoke
                          ▼
        +------------------------------------------------+
        |                 Servlet                        |
        +------------------------------------------------+
                          │
       (2) Invokes the particular Servlet
                          ▼
        +------------------------------------------------+
        |                 Response                       |
        +------------------------------------------------+
```



## Problem with Servlet:
1. web.xml becomes too complicated, spring framework removes that.
2. Spring introduced annotations based configuration.
3. Inversion of control: provided dependency injection.
4. difficult to manage rest api's.


## Spring MVC : 
Spring MVC, as many other web frameworks, is designed around the front controller pattern where a central `Servlet`, the `DispatcherServlet`, provides a shared algorithm for request processing, while actual work is performed by configurable delegate components. This model is flexible and supports diverse workflows.
### Inversion of control (IoC):
-> Before IoC and dependency injection, there was very tight coupling between objects. We needed to manage the objects.

--> IoC means, I am not managing the dependencies, control is to the spring framework.
--> the dependency injection is achieved through the IoC.
--> Spring framework manages the creation as well as life cycle of the object. It also manages the injection of it.


![[spring-intro.png]]

1. `@EnableWebMvc` used to enable web mvc application
2. `@ComponentScan(basePackages = com.xyz,....)` 
3. We also need instance of dispatcher servlet by entending it....


## Spring Boot 
provides ...
1. Dependency management 
2. Auto configuration (Opinionated..) Convention over configuration.
3. Inbuilt Embedded server (tomcat/jetty), In traditional spring MVC application, we need to create JAR/WAR of application and deploy it to the servlet container, but spring boot provides embedded servlet container, we just run app and it does it automatically.

# References
