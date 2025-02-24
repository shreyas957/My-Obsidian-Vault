2025-02-21 19:22

Status:

Tags:


# Fundamentals Of Back-end Engineering


# Backend Communication Design Patterns

## 1. Request - Response Model: 
- Process: 
	- Client sends request
	- Server parses the request
	- Server process the request
	- Server send a response
	- Client parses the response and consume
- Where it is used? 
	- Web, HTTP, DNS,SSH.....
	-  RPC (Remote procedure call) --> Execute method which is across different machine.
	- SQL and Database protocols.
	- APIs(REST/SOAP/GraphQL)
- Anatomy of request/ response: 
	-  A request structure is defined by both client and server.
	- Request has boundary.
	- Defined by a protocol and mes format. We need to parse the request, the both client and server should agree on same thing.
	- Same for response.
	- E.g. HTTP Request
```txt
GET / HTTP/1.1
Headers
<CRLF>
BODY
```
- Building an upload image service with request response.
	- Send large request with the image(single)
	- Chunk image and send a request per chunk(resumable).
	- Problem with 1st one will be if it fails in any parts we need to do it again, where as in 2nd part, we mark each chunk  with unique identifier, server can explicitly say I have these chunks send me specific one which I don't have.
- Doesn't work everywhere...
	- Notification service --> I want to get notified when someone log in, but here client doesn't really know that, Server need to check constantly, Do I have notification?.... 
	- Chatting App --> We can try request-response, But I need to make request again and again to check if message is there, which doesn't really work! These empty requests will congest the network.
	- Very Long requests.
	- What if client disconnect?.... 




# References
