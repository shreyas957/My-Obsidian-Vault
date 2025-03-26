2025-03-26 09:43

Status:

Tags:


# Controller Layer Annotations
## Annotations: 
1. `@Contoller`: Marks the class to handle incoming http requests.
2. `@RestController`: Combinations of `@Controller` & `@ResponseBody`
3. `@ResponseBody`: It tells that return type of method is considered as http response. If we don't write it, Spring Boot try to resolve it as view(html, jsp, etc).
4. `@RequestMapping`: Matches the url path to specific method. Can be written at class level too, so that all paths defined in the class will be prefixed with it.
```java
@RequestMapping(path = "/home", method = RequestMethod.GET, produces = MediaType.TEXT_PLAIN_VALUE)
// other parameters are there also....
```
5. `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping` are specialised types of `@RequestMapping` annotation.
6. `@RequestParam`: It helps bind request parameters to controller method parameter.
	for http://localhost:8080/api/fetchUser?firstName=Shreyas&lastName=Shevale&age=28
	Passed as arguments to method, Make sure to have same name for variable as well as param name. It can be either required or can not required as well. 
	It supports the type-conversion from String representation of path to specified type me method. (primitive, wrapper, String, Enums, Custom objects--> Using PropertyEditor --> By extending PropertyEditorSupport)
7. `@InitBinder`: For each method whenever any API get invoked, first run this binder and check if any of it's parameters required any processing. (It takes 3 parameters, return type, parameter name, and propertyEditor instance)
8. `@PathVariable`: Used to extract the values from the path of the URL and help to bind it to the controller method parameter.
	The path name and variable name should be same.
```java
@GetMapping("/rest/{name}")  
public String rest(@PathVariable String name) {  
    return "Hello " + name;  
}
```
9. `@RequestBody`: Bind the body of HTTP request(typically JSON) to the controller method parameter(Java Object).
	It allow us to pass the object as requests body. It automatically parse the json to java object. We can use `@JsonProperty` to have custom name in json body for key, which allow use to pass values for the key as same as variable name or our defined key for the variable.
10. `@ResponseEntity`: It represents the entire HTTP response, Including header, status, response body, etc. which can be sent to client. I can set everything such as authorization code, httpStatus code, etc.....
    If am I returning the String then SB automatically creates the ResponseEntity of that type behind the scene. 
```java
@GetMapping("/fetchUserName")  
public ResponseEntity<String> fetchUSer(@RequestParam(name = "firstName") String firstName, @RequestParam(name = "lastName", required = false) String lastName) { 
    return ResponseEntity.status(HttpStatus.OK).body(firstName);  
}
```










# References
