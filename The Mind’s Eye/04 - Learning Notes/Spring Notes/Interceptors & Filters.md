2025-11-24 21:13

Status: [[complete]]

Tags: [[Spring Boot]]


# Interceptors & Filters

![[spring-boot-interceptor-filter.png]]

## 1. Interceptor:
It is a mediator, which gets invoked before or after your actual code.
Specific to spring framework, Intercept the HTTP request & response, before they reach to the controller.S 

1. Simplest way to create interceptor is to extend class by `HandlerInterceptor` and override methods.
2. And add that to `WebMvcConfigurer`


## 2. Custom interceptor for requests after reaching to specific controller:
1. Create a custom annotation
2. Then use that annotation on methods where we want to invoke interceptor.
3. Now we can use AOP to write some logic before and after the method execution. (this isn't actual interceptor though)



## 3. Filter:
It intercept the HTTP request and response, before they reach to the servlet.

- Servlet is nothing but java class, which accepts the incoming request, process it and returns the response.
- Filters can be register by `FilterRegistrationBean` bean.

- Filter is used when we want to intercept the request and response and add logic agnostic to the underlying servlet. 
  We can have many filter as we want, and have ordering between them.
  e.g. Adding logic of checking JWT token.
- Interceptors are used when we want to intercept the HTTP request and response and add logic specific to a particular servlet. We can have as many as we want and order them.


# References
