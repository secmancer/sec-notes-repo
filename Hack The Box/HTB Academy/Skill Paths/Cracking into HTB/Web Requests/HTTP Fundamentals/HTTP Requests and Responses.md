### Basic Idea
- HTTP communications consist of an HTTP request sent by the client (e.g., cURL or browser) and processed by the server (e.g., web server).
- The request includes details like URL, path, parameters, request data, headers, and other options, which will be discussed throughout this module.
- Upon receiving the request, the server processes it and sends an HTTP response, containing the response code (covered later) and resource data if access is granted.

### HTTP Request
- The image above shows an HTTP GET request to the URL:
	- `http://inlanefreight.com/users/login.html`
- The first line of any HTTP request contains three main fields 'separated by spaces':
![[Screenshot_20241107_154749.png]]
- The next set of lines contains HTTP header value pairs like `Host`, `User-Agent`, `Cookie`, etc., which specify attributes of a request.
- These headers are terminated with a new line, essential for the server to validate the request.
- A request may also include a request body with data, which is sent along with the headers.

> **Note:** HTTP version 1.X sends requests as clear-text, and uses a new-line character to separate different fields and different requests. HTTP version 2.X, on the other hand, sends requests as binary data in a dictionary form.


### HTTP Response
- The first line of an HTTP response includes the `HTTP version` (e.g., `HTTP/1.1`) and the `response code` (e.g., `200 OK`).
- Response codes indicate the status of the request, as discussed in later sections.
- After the first line, response headers follow a similar format as requests.
- The response may end with a `response body`, which is usually `HTML` but can also be other formats like `JSON`, images, styles, scripts, or documents like PDFs.


### cURL
- In previous cURL examples, we only specified the URL to get the response body.
- cURL also supports displaying the full `HTTP request` and `response`, useful for web penetration tests and writing exploits.
- Use the `-v` verbose flag to view both the request and response.
```shell-session
secmancer@htb[/htb]$ curl inlanefreight.com -v

*   Trying SERVER_IP:80...
* TCP_NODELAY set
* Connected to inlanefreight.com (SERVER_IP) port 80 (#0)
> GET / HTTP/1.1
> Host: inlanefreight.com
> User-Agent: curl/7.65.3
> Accept: */*
> Connection: close
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 401 Unauthorized
< Date: Tue, 21 Jul 2020 05:20:15 GMT
< Server: Apache/X.Y.ZZ (Ubuntu)
< WWW-Authenticate: Basic realm="Restricted Content"
< Content-Length: 464
< Content-Type: text/html; charset=iso-8859-1
< 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>

...SNIP...
```
- The `-v` flag shows the full HTTP request and response.
- The `GET / HTTP/1.1` request included headers like `Host`, `User-Agent`, and `Accept`.
- The `401 Unauthorized` response indicates lack of access to the resource.
- The response also included headers like `Date`, `Content-Length`, and `Content-Type`.
- The response body remained the same as without the `-v` flag.


> **Exercise:** The `-vvv` flag shows an even more verbose output. Try to use this flag to see what extra request and response details get displayed with it.


### Browser DevTools
- Browser DevTools are essential for web penetration testing, providing tools for assessing web requests.
- DevTools can be accessed with [`CTRL+SHIFT+I`] or [`F12`] in Chrome or Firefox.
- The main focus in this module is the `Network` tab, which shows web requests and responses.
- The `Network` tab displays response status codes, request methods (`GET`), requested URLs, and paths.
- The `Filter URLs` feature helps narrow down specific requests when dealing with numerous loaded resources.

> **Exercise:** Try clicking on any of the requests to view their details. You can then click on the `Response` tab to view the response body, and then click on the `Raw` button to view the raw (unrendered) source code of the response body.


### Questions
- What is the HTTP method used while intercepting the request? (case-sensitive)
	- GET
- Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)
	- 2.4.41