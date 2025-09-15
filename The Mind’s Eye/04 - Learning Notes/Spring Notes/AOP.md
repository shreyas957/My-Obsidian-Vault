2025-09-15 10:30

Status: [[Spring Boot]]

Tags: [[complete]]


## Aspect Oriented programming: 
In simple terms it helps to intercept method invocation, and do something before and after it.
- It helps us to reduce boilerplate & repetitive code  such as logging, transaction management, etc.
- And **Aspect** handles this boilerplate for us. 
- helps in reusability and maintainability of code.
- `spring-boot-starter-aop` is used as dependency.

---
## AOP Concepts

- **Aspect:** A modular unit for a cross-cutting concern (e.g., logging, transaction management). Implemented as a regular class, sometimes with the `@Aspect` annotation.
    
- **Join Point:** A specific point in a program's execution, like a method call. In Spring, it's always a method execution.
    
- **Advice:** The action taken by an aspect at a join point. Think of it as an interceptor. Types include **Before**, **After Returning**, **After Throwing**, **After (finally)**, and **Around** advice.
    
- **Pointcut:** A predicate that selects where advice should run. It defines which join points to match (e.g., all methods with a certain name).
    
- **Introduction:** Adding new methods or interfaces to an existing object.
    
- **Target Object:** The object being advised by one or more aspects.
    
- **AOP Proxy:** The object created by the AOP framework to apply advice.
    
- **Weaving:** The process of linking aspects to other objects to create an advised object. Spring AOP does this at runtime.
---
## Advice Types

- **Before:** Runs before a method, but can't stop it unless it throws an exception.
    
- **After Returning:** Runs after a method completes successfully.
    
- **After Throwing:** Runs after a method throws an exception.
    
- **After (finally):** Runs no matter how a method exits (normally or with an exception).
    
- **Around:** The most powerful. It wraps a method call and can perform actions before and after, or even prevent the original method from running. Use the most specific advice type possible to avoid errors.
---
##### **`@Aspect`** : 
It marks a class as an Aspect.  By annotating a class with `@Aspect`, you are telling the Spring Framework that this class contains the logic for a cross-cutting concern. Spring will then detect this class and use it to configure AOP proxies.

```java
@Before("execution(public String dev.shreyas.Controller.aop())")
```
1.  public is access modifier and it is optional & can be omitted
2. String --> Return type, optional but cant be omitted
3. `dev.shreyas.Controller.aop()` --> Pointcut
4. `@Before()` & the method together it is called Advice 

##### **Execution** :
- matches particular method in particular class.
- **(\*)  wildcard** : matches any single item
	- e.g.  `@Before("execution(* dev.shreyas.Controller.aop())")` --> Matches any return type
	- `@Before("execution(* dev.shreyas.Controller.*(String))")`  --> Matches any method with String as parameter.
	- `@Before("execution(* dev.shreyas.Controller.aop(*))")`  --> matches to aop method with any single parameter.
- **(..) wildcard**: matches 0 or more items:   
	- `@Before("execution(* dev.shreyas.Controller.aop(..))")` -->  matches aop method that takes 0 or more parameters. 
	- `@Before("execution(* dev.shreyas.Controller..())")` --> matches to any method in package `dev.shreyas.Controller` or sub-packages.  
##### **Within**:  
- Matches all methods within any package or class.
- e.g. `@Before("within(dev.shreyas.Controller)")` -->  This pointcut will run for each method in Controller class.
- `@Before("execution(* dev.shreyas..*")` --> this will run for all methods for shreyas package and it's sub-package. 
##### **@within**: 
- Matches any method in a class which has the specified annotation.
- e.g. `@within(org.springframework.stereotype.Service)` --> Matches to all the methods of class which is Annotated with @Service. 
##### **@annotation** : 
- Matches any method which is annotated with given annotation.
- e.g. `@annotation(org.springframework.web.bind.annotation.GetMapping)`
##### **args**: 
- Matches any method with particular arguments(or parameters) 
- e.g. `@Before("args(String, int)")` -->  Matches to method which takes String and int as parameter. 
- In case of Object type we need to give fully qualified name of the type. 
  e.g. `@Before("args(com.shreyas.entity.Employee)")` --> match to method which takes Employee as parameter. 
##### **@args**:  
- matches any method with particular parameters and that parameter class is annotated with particular annotation.
- e.g.  `@args(org.springframework.stereotype.Service)`  --> It matches to the method which takes a type(class for example) as parameter which is annotated with @Service.  
##### **target**: 
- Matches any method on particular instance of class.
- 










# References
