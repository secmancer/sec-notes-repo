### Introduction
- We’ve seen examples of HTTP requests and response headers in earlier sections.
- HTTP headers transfer information between the client and server.
- Some headers are specific to requests or responses, while others are commonly used in both.
- Headers can have one or multiple values, appended after the header name and separated by a colon. 
- We can divide headers into the following categories:
	1. `General Headers`
	2. `Entity Headers`
	3. `Request Headers`
	4. `Response Headers`
	5. `Security Headers`


### General Headers
- [General headers](https://www.w3.org/Protocols/rfc2616/rfc2616-sec4.html) are used in both HTTP requests and responses. They are contextual and are used to `describe the message rather than its contents`.
![[Screenshot_20241107_155026.png]]


### Entity Headers
- Similar to general headers, [Entity Headers](https://www.w3.org/Protocols/rfc2616/rfc2616-sec7.html) can be `common to both the request and response`. These headers are used to `describe the content` (entity) transferred by a message. They are usually found in responses and POST or PUT requests.
![[Screenshot_20241107_155048.png]]


### Request Headers
- The client sends [Request Headers](https://tools.ietf.org/html/rfc2616) in an HTTP transaction. These headers are `used in an HTTP request and do not relate to the content` of the message. The following headers are commonly seen in HTTP requests.
![[Screenshot_20241107_155114.png]]


### Response Headers
- [Response Headers](https://tools.ietf.org/html/rfc7231#section-7) can be `used in an HTTP response and do not relate to the content`. Certain response headers such as `Age`, `Location`, and `Server` are used to provide more context about the response. The following headers are commonly seen in HTTP responses.
![[Screenshot_20241107_155138.png]]


### Security Headers
- Finally, we have [Security Headers](https://owasp.org/www-project-secure-headers/). With the increase in the variety of browsers and web-based attacks, defining certain headers that enhanced security was necessary. HTTP Security headers are `a class of response headers used to specify certain rules and policies` to be followed by the browser while accessing the website.
![[Screenshot_20241107_155203.png]]

> **Note:** This section only mentions a small subset of commonly seen HTTP headers. There are many other contextual headers that can be used in HTTP communications. It's also possible for applications to define custom headers based on their requirements. A complete list of standard HTTP headers can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers).


### cURL
- In the previous section, we used the `-v` flag with cURL to view detailed HTTP requests and responses.
- To view only response headers, use the `-I` flag to send a `HEAD` request.
- The `-i` flag displays both headers and the response body (e.g., HTML code).
- The key difference is that `-I` sends a `HEAD` request, while `-i` sends a regular request with headers.
```shell-session
secmancer@htb[/htb]$ curl -I https://www.inlanefreight.com

Host: www.inlanefreight.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/605.1.15 (KHTML, like Gecko)
Cookie: cookie1=298zf09hf012fh2; cookie2=u32t4o3tb3gg4
Accept: text/plain
Referer: https://www.inlanefreight.com/
Authorization: BASIC cGFzc3dvcmQK

Date: Sun, 06 Aug 2020 08:49:37 GMT
Connection: keep-alive
Content-Length: 26012
Content-Type: text/html; charset=ISO-8859-4
Content-Encoding: gzip
Server: Apache/2.2.14 (Win32)
Set-Cookie: name1=value1,name2=value2; Expires=Wed, 09 Jun 2021 10:18:14 GMT
WWW-Authenticate: BASIC realm="localhost"
Content-Security-Policy: script-src 'self'
Strict-Transport-Security: max-age=31536000
Referrer-Policy: origin
```

> **Exercise:** Try to go through all of the above headers, and see whether you can recall the usage for each of them.

- In addition to viewing headers, cURL also allows us to set request headers with the `-H` flag.
- Some headers, like the `User-Agent` or `Cookie` headers, have their own flags. 
- We can use the `-A` to set our `User-Agent`.
```shell-session
secmancer@htb[/htb]$ curl https://www.inlanefreight.com -A 'Mozilla/5.0'

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```

> **Exercise:** Try to use the `-I` or the `-v` flags with the above example, to ensure that we did change our User-Agent with the `-A` flag.


### Browser DevTools
- Finally, we can view HTTP headers using browser devtools by navigating to the `Network` tab.
- In the `Headers` tab, we can see both HTTP request and response headers, arranged into sections.
- Clicking the `Raw` button displays the headers in their raw format.
- The `Cookies` tab allows us to view any cookies used in the request, as discussed in upcoming sections.


### Questions
- The server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.
	- HTB{p493_r3qu3$t$_m0n!t0r}