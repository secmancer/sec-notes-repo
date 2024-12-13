### Introduction
- HTTP supports multiple methods for accessing a resource. In the HTTP protocol, several request methods allow the browser to send information, forms, or files to the server.
- These methods are used, among other things, to tell the server how to process the request we send and how to reply.
- We saw different HTTP methods used in the HTTP requests we tested in the previous sections.
- With cURL, if we use `-v` to preview the full request, the first line contains the HTTP method (e.g. `GET / HTTP/1.1`), while with browser devtools, the HTTP method is shown in the `Method` column.
- Furthermore, the response headers also contain the HTTP response code, which states the status of processing our HTTP request.


### Request Methods
- The following are some of the commonly used methods:
![[Screenshot_20241107_155419.png]]
- The list only highlights a few of the most commonly used HTTP methods. 
- The availability of a particular method depends on the server as well as the application configuration. 
- For a full list of HTTP methods, you can visit this [link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).

> **Note:** Most modern web applications mainly rely on the `GET` and `POST` methods. However, any web application that utilizes REST APIs also rely on `PUT` and `DELETE`, which are used to update and delete data on the API endpoint, respectively. Refer to the [Introduction to Web Applications](https://academy.hackthebox.com/module/details/75) module for more details.


### Response Codes
- HTTP status codes are used to tell the client the status of their request. An HTTP server can return five types of response codes.
![[Screenshot_20241107_155449.png]]
- The following are some of the commonly seen examples from each of the above HTTP method types.
![[Screenshot_20241107_155507.png]]
- For a full list of standard HTTP response codes, you can visit this [link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). 
- Apart from the standard HTTP codes, various servers and providers such as [Cloudflare](https://support.cloudflare.com/hc/en-us/articles/115003014432-HTTP-Status-Codes) or [AWS](https://docs.aws.amazon.com/AmazonSimpleDB/latest/DeveloperGuide/APIError.html) implement their own codes.