2025-03-24 20:01

Status: [[Spring Boot]]

Tags: [[complete]]


# Spring Boot Layered Architecture
## Project Setup: 
1. Group name : generally our organisations domain name in reverse
2. ArtifactId : project name
## Layered Architecture:
![[SB_Layered_Arch.png]]
1. DTO : (RequestDTO/ResponseDTO) Data transfer object are used when we don't want to expose our entities, which makes our application much secure.
2. Utility: Helper methods which are used in our application and not in specific part.
3. Entity: It is the object(POJO) which represents the actual table in DB.
4. Configuration: We can configure application via properties file or, we can have java configuration file as well.









# References
