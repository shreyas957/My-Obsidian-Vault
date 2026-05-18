2025-12-14 19:01

Status: [[complete]]

Tags: [[Spring Boot]]



## HATEOAS: 
**H**ypermedia **A**s **T**he **E**ngine **O**f **A**pplication **S**tate


![[Hateoas-ex1.png]]

## When and Why use HATEOAS? 
- Purpose: 
  1. Loose coupling
  2. API discovery
To achieve above, server provides the next set of API's (Actions) in the response itself. Which client take. So that client have less business logic around API(Which api to invoke, how to invoke and when to invoke).

But adding all next set of actions can make API response bloat and has several disadvantages.
- Increased complexity at server side.
- Latency impact
- Increased payload size. 

- Never add all possible set of actions(API)
- So wee need to do proper analysis to achieve **Loose Coupling**

![[Hateoas-ex2.png]]

We can see in above diagram tight coupling in verify process.
Client needs some info before it can decide which verify api to invoke.
```JSON
{
	"userID": "12345",
	"name": "Shreyas",
	"verifyStatus": "UNVERFIED",
	"verifyType": "SMS",
	"verifyState": "NOT_YET_STARTED"
}
```

Based on this response client needs business logic to verify user (assume if else conditions).

```
if(VerifyStatus == "UNVERIFIED")
{
  if(verifyType== "SMS")
  {
    if(verifyState== "NOTE_YET_STARTED")
    {
      Call POST: /sms-verify-start
    }
    Else if (verifyState == "STARTED")
    {
      Call POST: /sms-verify-finish
    }
  }
  Else if(verifyType == "EMAIL")
  {
    if(verifyState== "NOTE_YET_STARTED")
    {
      Call POST: /email-verify-start
    }
    Else if (verifyState == "STARTED")
    {
      Call POST: /email-verify-finish
    }
  }
}
```


This can be removed
```JSON
{
	"userID": "12345",
	"name": "Shreyas",
	"verifyStatus": "UNVERFIED",
	"links": [
		{
			"rel": "verfiy",
			"href": "http://localhost:8080/api/sms/verify-start/12345",
			"type": "POST"
		}
	]
}
```
Now business logic is: 
```
if(VerifyStatus == "UNVERIFIED") {
	// Invoke the HATEOAS verify link given.
}
```

# References
