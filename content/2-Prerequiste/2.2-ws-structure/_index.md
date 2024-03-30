---
title : "Web Server Structure"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2. </b> "
---

#### Web Server Structure

![ws-structure](/images/2.2-ws-structure/00001.jpg?featherlight=false&width=60pc)
The structure of a web server can be divided into the following basic components:
1. Server Hardware:
> * **Server**: A computer that runs continuously to serve web services.
> * **Network Connectivity**: To connect to the internet or an internal network.
2. Server Software:
> * **Operating System**: Typically variants of Linux (such as Ubuntu, CentOS) or Windows Server.
> * **Web Server Software**: Software running on the server to handle HTTP requests. Apache, Nginx, Microsoft IIS are common examples.
3. Applications and data:
> * **Web Application**: The source code of the website or web application, often written in languages such as HTML, CSS, JavaScript, and backend languages like PHP, Python, Ruby, or Node.js.
> * **Data**: Databases are commonly used to store data for web applications, such as MySQL, PostgreSQL, MongoDB.

The operation of a web server can be outlined as follows:
1. Request Reception:
> * The web server listens on a specific port (typically port 80 for HTTP or 443 for HTTPS).
> * When an HTTP request is sent, the web server receives this request via the TCP/IP protocol.
2. Request Processing:
> * The web server identifies the type of request (GET, POST, PUT, DELETE) and parses the Uniform Resource Identifier (URI).
> * Based on the URI and configuration rules, the web server determines what to do with the request (e.g., access a file, execute source code, send back a previously stored webpage)
3. Response Generation:
> * Based on the request type and content, the web server generates an HTTP response.
> * This response could be an HTML page, a file, or a status code
> * The response is sent back to the client via the TCP/IP protocol.
4. Connection Closure:
> * After the response is sent, the TCP/IP connection may be closed or kept alive to support keep-alive (keeping the connection open to reduce latency in establishing new connections).
5. Logging and Monitoring:
> * The web server may log information about processed requests and server activity for analysis and performance monitoring purposes.
