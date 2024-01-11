---
title: All About HTTP (Hyper Text Transfer Protocol)
date: 2024-01-10 10:00:00 -500
categories: [client-server]
tags: [http]
---

## HTTP Anatomy
It's Client/Server Architecture. Client (Browser) sends HTTP Request to the Server and then Sever respond back to the Client with HTTP Response.
- (Client) Browser, Python or JavaScript app, or any app that makes HTTP Request.
- (Server) HTTP Web Server, eg. IIS (Internet Information Services), Apache Tomcat, NodeJS, Python Tornado.

### HTTP Request

| Format | Description |
| --- | --- |
| URL | The URL which Locate to HTTP Server |
| Method Type | POST, GET, PUT, DELETE |
| Headers | The context behind the payload like Cookies, Proxy etc... |
| Body | Actual Payload (GET won't have body...) |

### HTTP Response

| Format | Description |
| --- | --- |
| Status Code | Status of Operation (200 - Success, 404 - Not Found, 400 - Bad Request) |
| Headers | The context behind the payload |
| Body | Actual Response Data (Payload) |

## How HTTP works?
- HTTP is Layer 7 Protocol that means it operates within the **application layer** of the Open Systems Interconnect (OSI) model.
- Like TCP is Layer 4 Protocol which is actually smart layer which transfer payload (blob data) by establishing TCP connection from source to destination and transfer data in terms of packets.
- TCP is little bit expensive because it needs to do lots of stuff like congestion control (traffic management), security stuff (cryptography), etc...

- Before getting request and sending request there is handshaking take place to establish secure connection between Client and Server.

## HTTP 1.0
- It was launched in 1996. at that time max capacity of RAM is 64 MB or around.

![HTTP1.0](https://github.com/omjogani/blogs/assets/72139914/d24fae3a-d1ab-4ce2-a1ef-1f1c39632155)

- TCP connection was expansive at that time. for each request we open connection with handshaking, then request-response takes place and close the connection.
- If we want to fire another request we again need to open that expansive TCP connection and request-response and close the connection. It's tedious & slow process to work with.
- So, HTTP 1.0 didn't sustain more than a year even.

## HTTP 1.1
- In 1997, HTTP 1.1 was launched. It is the only protocol that survive around 20 Years. then HTTP 2.0 takes place.

![HTTP1.1](https://github.com/omjogani/blogs/assets/72139914/947396d6-4539-40bc-b96d-d5b15d9a9096)

- It solves a major issue which was there in HTTP 1.0 which was it needs to establish the connection for each request.
- In HTTP 1.1 It solve the issue by persisting that connection between Client & Server.
- For Persistent It uses caches, etag. That ultimately helps to reduce down latency.
- It also provide streaming with chunked transfer.

