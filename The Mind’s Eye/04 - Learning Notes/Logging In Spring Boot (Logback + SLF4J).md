2025-01-22 09:49

Status: [[complete]]

Tags: [[Java]] [[Spring Boot]]


# Logging In Spring Boot


### Types Of Frameworks :
1. Logback + SLF4J -> It comes by default with spring boot, SLF4J is abstraction of Logback.
2. Log4j2 -> It is a framework, also support, asynchronous logging
3. java.util.Logging -> Built in logging in jdk, very basic logging support.
### Customization : 
To customize the default configuration we can use `yaml` ,`spring-logback.xml` or `logback.xml` files in resources folder. 

### Logging Levels :
1. TRACE
2. DEBUG
3. INFO
4. WARN
5. ERROR
- By default DEBUG and TRACE is not enabled.
- Logback does not have  `FATAL` level --> corresponds to `ERROR`
- Log consist of 
	- Date and Time: Millisecond precision and easily sortable.
	- Log Level: `ERROR`, `WARN`, `INFO`, `DEBUG`, or `TRACE`.
	- Process ID.    
	- A `---` separator to distinguish the start of actual log messages.
	- Application name: Enclosed in square brackets (logged by default only if `spring.application.name` is set)
	- Application group: Enclosed in square brackets (logged by default only if `spring.application.group` is set)
	- Thread name: Enclosed in square brackets (may be truncated for console output).
	- Correlation ID: If tracing is enabled (not shown in the sample above)
	- Logger name: This is usually the source class name (often abbreviated).
	- The log message.
	
- #### `TRACE` < `DEBUG` < `INFO` < `WARN` < `ERROR` < `OFF`
	If you set the logger level to `INFO`, the following levels are also considered:
	- `INFO` will be logged.
	- `WARN` and `ERROR` will also be logged (since they are more critical).
	- `TRACE` and `DEBUG` will **not** be logged (since they are less critical).
	If you set the logger level to `WARN`:
	- `WARN` and `ERROR` will be logged.
	- `INFO`, `DEBUG`, and `TRACE` will **not** be logged.

- We can set desired logging levels to specific packages or classes, allowing them to control logging information at runtime.
### Logging Info : 
1. Spring boot provides annotations like @Slf2j and Log4j2 to directly inject logger instance in our class.
2. We can create logger for specific class by
```java
private static final Logger logger = LoggerFactory.getLogger(MyClass.class);
logger.info("HI");
logger.error("Hi {}", user, e) // Here {} will be replace by user as place-holder
```

- For complete project
```yml
logging:
	level:
		root: OFF/TRACE/....
# For perticuler package
logging:  
  level:  
    com:  
      nexuside: TRACE
# Same way we can control logs of perticuler class also
```


### More On logback.xml :
Generally it is used because it gives separation between out spring configuration in yaml and logging config in xml file.

- `<configuration>  </configuration>` is root element of our logback.xml file.All configuration is inside it.
- `<appender> </appender>` : Means where I want to print the logs. e.g. to console or to file
- Loggers : 



# References

