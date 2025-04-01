2025-02-21 19:22

Status:

Tags: [[CORE CS]]


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

## 2. Synchronous vs Asynchronous   
(Can I do work while waiting?)
Synchronous --> Step by step one by one execution 
Asynchronous --> I'll do something else while waiting for response. 
1. Synchronous I/O : 
	- Caller sends requests and blocks. (thus our running process is context switched by another process)
	- Caller cannot execute any code meanwhile
	- Receiver responds, caller unblocks
	- Thus caller ans receiver are in 'sync'
2. Asynchronous I/O : 
	- Caller sends a request
	- Caller can work until it gets a response 
	- Caller either -> 
		1. Check if the response is ready (epoll)
		2. Receiver calls back when its done (io_uring)
		3. Spins up a new thread that blocks (someone else do it)
	- Caller and receiver are not in sync
 
3. Asynchronous workload is everywhere -->
	- **Asynchronous back-end programming**, technically backend thinks someone is waiting for my response right....to the backend whoever called the particular service, it is synchronous, what trick we can do is, **USE of QUEUE's**, If client sends request, will not process it immediately, will put it in queue, and tell to client with response of job-id, client will check the status of request later.
	-  **Asynchronous commits in postgreSQL**, in postgres, whatever changes we do, read, write, update or delete they are stored in logs as _WAL (write ahead log)_. thus in-case of crash, we can recover the database. We we say commit, postgres will call it synchronously, postgres will only unblock when WAL is saved to disk and return result. In case of _Asynchronous commit_ is an option that allows transactions to complete more quickly, (we return result before even WAL is saved in disk) at the cost that the most recent transactions may be lost if the database should crash. In many applications this is an acceptable trade-off.
	- Asynchronous replication --> have primary writter and many secondary readers. 

## 3. Push: 
Request/response isn't always ideal....what if?
- Client wants real time notification from backend.
- In this use case push model is good such as chatting.
- Push means if something is available backend push it to client.

1. What is Push?
	- Client connects to server.
	- Server sends data to client.
	- Client doesn't have to request anything.
	- Protocol must be bi-direction.(uni is also okay)
	- Used by *RabbitMQ*
	- It is real time
	- Con is that Client must be connected to server, Client might not be able to handle, polling is preferred for light clients. 
	- We can use *WebSockets* for it.  

## 4. Short Polling: 
(Request is taking a while, I'll check with you later)
Request/Response isn't ideal when a request takes a long time to process or backend wants to send a notification. 
Polling is good communication style.
1. What is short polling?
	- Clients send request.
	- Server responds immediately with handle(handle is basically a unique identifier which corresponds to specific request)
	- Server is free to do something else or process the request.
	- Client uses that handle to check for status.
	- multiple "Short" request-response as polls.
	- Pros: It is simple and good for long running requests. Client can disconnect(persist the handle).
	- Cons: It's too chatty(many requests), high consumption of network bandwidth and wasted resources.

## 5. Long Polling:
(Request is taking long, I'll check with you later but talk to me only when it's ready)
1. What is long polling?
	- Client sends Request
	- Server responds immediately with handle
	- Server Continues to process the request.
	- Client uses that handle to check for status
	- *Server does not reply until it has the response(unlike short polling where server responds even though response is not available)*
	- Kafka uses this
	- Some variations can have timeouts too.
	- Not real time.

## 6. Server Sent Events:
(One request, a very very long response)
- Server sent events works with request/response.
- Designed for HTTP, works in web.
1. What is SSE? 
	- A response has start and end.
	- Client sends a Request.
	- Server sends logical events as a part of response
	- Server never writes the end of the Response
	- It is still a request but an unending response.
	- Client parses the streams data looking for events.
	- Content type of reques is *text/event-stream*
	- Pros: It is real time and compatible with req/res.
	- Cons: Client must be offline, or might not be able to handle.
	- Cons: HTTP/1.1 problem (6 Connections)

## 7. Publish Subscribe (Pub/Sub):
(One publisher, many readers)
- Request/Response is bad for multiple receivers, and has high coupling. 
- Client/Server has to be running
- Chaining, circuit breaking
![[pub-sub.png]]
- Pros: 
	- Scales w.r.t multiple receivers
	- Great for microservices
	- Loose coupling
	- Works while clients not running.
- Cons: 
	- Message delivery issues(two generals problem)
	- complexity
	- Network saturation


## 8. Multiplexing vs Demultiplexing: 
(HTTP/2, QUIC, Connection Pool, MPTCP)
1. Multiplexing & Demultiplexing: 
![[Multiplexing-1.png]]
![[Multiplexing-2.png]]
![[Demultiplexing.png]]
- Chrome allows up to 6 connections per domain. other will be blocked.

2. Connection Pooling: 
	We establish a number of connections and keep them hot. 
	Whenever a request comes, use one of the free connection. 
	- If a new request comes then we make new connection(under limit)
	- But for new request limit of connection pool is reached, then the request will be blocked, until a connection is free to use. 

































# References
