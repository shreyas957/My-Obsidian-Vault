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
## Advice Types : 
An **advice** is the **action that is taken** at a particular point in the program execution
- **Before:** Runs before a method, but can't stop it unless it throws an exception.
- **After Returning:** Runs after a method completes successfully.
- **After Throwing:** Runs after a method throws an exception.
- **After (finally):** Runs no matter how a method exits (normally or with an exception).
- **Around:** The most powerful. It wraps a method call and can perform actions before and after, or even prevent the original method from running. Use the most specific advice type possible to avoid errors.
---
## **`@Aspect`** : 
It marks a class as an Aspect.  By annotating a class with `@Aspect`, you are telling the Spring Framework that this class contains the logic for a cross-cutting concern. Spring will then detect this class and use it to configure AOP proxies.

```java
@Before("execution(public String dev.shreyas.Controller.aop())")
```
1.  public is access modifier and it is optional & can be omitted
2. String --> Return type, optional but cant be omitted
3. `dev.shreyas.Controller.aop()` --> Pointcut
4. `@Before()` & the method together it is called Advice 
---
## Pointcut Designators: 
`execution(modifiers-pattern? return-type-pattern declaring-type-pattern? method-name-pattern(param-pattern) throws-pattern?)`
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
- Matches any method in a class which has the specified annotation. (class level)
- e.g. `@within(org.springframework.stereotype.Service)` --> Matches to all the methods of class which is Annotated with @Service. 
##### **@annotation** : 
- Matches any method which is annotated with given annotation.  (method level)
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
- e.g.  `@args(dev.shreyas.util.EmployeeUtil)`
- We can also specify the interface, and It's implementations bean will be used.
##### **@target**: 
- Any method on a bean whose class is annotated with specified annotation. 
- It works at runtime so it is proxy aware and works on inherited methods as well.

 `@target / target` → Think Target → Time of execution → Runtime

---
## Combining two pointcuts:
We can combine using  **&&**  , **| |**  
e.g. `@Before("execution(* dev.shreyas.controller.EmployeeController.*()) && @annotation(org.springframework.web.bind.annotation.GetMapping)")`

---
## Named Pointcut: 
A **named pointcut** is a way to **extract and reuse** a pointcut expression by giving it a **name**. It improves **readability**, **maintainability**, and **reusability** of your AOP logic — especially when you're using the same expression in multiple advice methods.
- The method marked with `@Pointcut` must be always empty, and its name becomes alias for pointcut expression.
- We don't call method, we just use its name in advice annotation.
e.g. 
```java
@Pointcut("execution(* com.example.service.*.*(..))")
public void serviceMethods() {
	// empty
}

@Before("serviceMethods()")
public void beforeAdvice() {
    System.out.println("Before service method");
}

// combined 
@Pointcut("execution(* com.example.service.*.*(..))")
public void serviceLayer() {}

@Pointcut("@annotation(org.springframework.transaction.annotation.Transactional)")
public void transactionalMethods() {}

@Pointcut("serviceLayer() && transactionalMethods()")
public void transactionalServiceMethods() {}
```
---
## @Around :
As name suggest, It surrounds the method execution(before and after). It is more powerful and can we used in many ways.
- We can run code before and after method.
- Modify the arguments
- Block or skip method execution
- Catch and handle exceptions
- Change return value
**`ProceedingJoinPoint`**  It is like pointer to method being intercepted. We can class `.proceed()` to continue method execution.
`.getArgs()` --> method arguments
`.getSignature()` --> method signature
`.getTarget()` -->target Object

|Rule|Explanation|
|---|---|
|Must return `Object`|Because you might intercept methods with different return types|
|Must throw `Throwable`|Because the method being intercepted might throw exceptions|
|Must call `proceed()`|Or else the original method will **not execute**|
```java
@Around("execution(* com.example..*(..))")
public Object measureTime(ProceedingJoinPoint joinPoint) throws Throwable {
    long start = System.currentTimeMillis();
    Object result = joinPoint.proceed();
    long duration = System.currentTimeMillis() - start;
    System.out.println(joinPoint.getSignature() + " executed in " 
    + duration + "ms");
    return result;
}
```

## How Does Method Interception Work in Spring AOP?
##### 1. **Proxy Creation**
- When Spring initializes your application context, it **wraps the target bean (the actual object)** with a **proxy object** if any aspects (advice) apply to it.
- This proxy implements the same interfaces as the target (if using JDK Dynamic Proxy) or subclasses the target class (if using CGLIB Proxy).
- The proxy **stands in place of the original object** when your application calls its methods.
##### 2. **Intercepting Method Calls**
- When a method is invoked on the proxy, **the call is intercepted first** by the proxy.
- The proxy checks if any advice (e.g., `@Before`, `@After`, `@Around`) matches the method based on the defined pointcut expressions.
##### 3. **Advice Execution**
- Depending on the advice type:
    - **`@Before` advice** runs before the actual method.
    - **`@After` advice** runs after the method finishes (successfully or with exception).
    - **`@Around` advice** wraps the method call and controls when or if the actual method executes.
- The advice can **access method arguments, modify them, handle exceptions, or alter the return value**.
##### 4. **Calling the Actual Method**
- In the case of `@Around` advice, the method execution proceeds when `proceed()` is called on the `ProceedingJoinPoint`.
- For other advice types, Spring ensures the original method executes at the appropriate time relative to the advice.
##### 5. **Return Control**
- After advice and the actual method execute, control returns to the caller.
- The proxy can modify or replace the return value or throw exceptions as needed.
---
## If We Have Hundreds of Pointcuts, Does Matching Happen Against All of Them on Every Method Call?
No, Spring AOP **does not match every method call against all pointcuts at runtime**. Instead, it uses a **proxy-based mechanism and caches** the matching pointcuts per bean or method to optimize performance.
- When Spring creates the proxy for a bean, it **analyzes the bean’s methods** against the defined pointcuts **once** during initialization.
- Only the methods that **match one or more pointcuts** are advised.
- This means the proxy knows **which advice to apply to which method upfront**
- At runtime, the proxy **does not scan all pointcuts again** on every method call.
- Instead, it directly invokes the advice linked to the method.
- This avoids expensive pointcut expression parsing or matching on every call.
When application startup happens:
1. Look for @Aspect annotation class
2. Parse the pointcut expressions (Done by PointcutPaser.java class)
3. Store in cache or efficient data structure.
4. Look for spring managed beans(e.g. @Component, @Service, etc..)
5. For each bean, it checks, if it is eligible for interception based on pointcut expression (AbstractAutoProxyCreator.java)
6. If yes, It creates proxy using **JDK Dynamic Proxy** or **CGLIB** proxy. This proxy class has code, which executes the advice before the method, then method execution happens and then any advice if there.

# References
