### **1. HTTP Communication Overview**
- HTTP communication consists of two main components:
	- **HTTP Request**: Sent by the client (e.g., browser or cURL) to the server.
	- **HTTP Response**: Sent by the server in reply to the client’s request.
- Both requests and responses contain specific fields, headers, and sometimes a body.



### **2. HTTP Request Anatomy**
- #### **Example HTTP GET Request**:
```
GET /users/login.html HTTP/1.1
Host: inlanefreight.com
User-Agent: curl/7.65.3
Accept: */*
```
- #### **Request Fields**:
	1. **Method**:
	    - Specifies the action to perform (e.g., `GET`, `POST`, `PUT`, `DELETE`).
	    - Example: `GET` retrieves the resource without altering server data.
	2. **Path**:
	    - The resource location on the server.
	    - Example: `/users/login.html`.
	    - May include a query string (e.g., `?username=user`).
	3. **Version**:
	    - Indicates the HTTP protocol version (e.g., `HTTP/1.1` or `HTTP/2`).
- #### **Request Headers**:
	- Key-value pairs that provide additional information about the request.
	- Common headers include:
	    - **Host**: Specifies the server’s domain (e.g., `inlanefreight.com`).
	    - **User-Agent**: Identifies the client making the request (e.g., `curl/7.65.3`).
	    - **Accept**: Specifies the types of content the client accepts (e.g., `text/html`).
- #### **Request Body**:
	- Optional; contains data for certain methods like `POST` or `PUT`.
	- Example: A `POST` request might include form data or JSON payloads.



### **3. HTTP Response Anatomy**
- #### **Example HTTP Response**:
```
HTTP/1.1 200 OK
Date: Tue, 21 Jul 2020 05:20:15 GMT
Server: Apache/X.Y.ZZ (Ubuntu)
Content-Type: text/html; charset=iso-8859-1
Content-Length: 464

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>...</head></html>
```
- #### **Response Fields**:
	1. **Version**: 
	    - Specifies the HTTP version used in the response (e.g., `HTTP/1.1`).
	2. **Status Code**:
	    - Indicates the status of the request (e.g., `200 OK`, `404 Not Found`).
- #### **Response Headers**:
	- Similar to request headers, they provide metadata about the response.
	- Common headers include:
	    - **Date**: Timestamp of the response.
	    - **Server**: Information about the server (e.g., `Apache`).
	    - **Content-Type**: Type of the response content (e.g., `text/html`).
- #### **Response Body**:
	- Contains the requested resource or data (e.g., HTML, JSON, images).



### **4. Using cURL to View HTTP Requests and Responses**
- #### **Basic Usage**:
```bash
curl http://example.com
```
- Retrieves the response body only.
- #### **Verbose Output**:
```bash
curl -v http://example.com
```
- Displays the full request and response, including headers and status codes.
- #### **Sample Output**:
```
> GET / HTTP/1.1
> Host: example.com
> User-Agent: curl/7.65.3
> Accept: */*

< HTTP/1.1 401 Unauthorized
< Date: Tue, 21 Jul 2020 05:20:15 GMT
< Server: Apache/X.Y.ZZ (Ubuntu)
< Content-Type: text/html; charset=iso-8859-1
...
```
- #### **Extra Verbose Output**:
```bash
curl -vvv http://example.com
```
- Displays even more detailed information about the request and response.



### **5. Using Browser DevTools**
- Built into modern browsers (e.g., Chrome, Firefox).
- Access via:
    - **Windows/Linux**: `[CTRL+SHIFT+I]` or `[F12]`.
    - **Mac**: `[CMD+OPT+I]`.
- #### **Network Tab**:
	- Tracks all web requests made by the browser.
	- Displays:
	    - Request method (e.g., `GET`, `POST`).
	    - Response status code (e.g., `200 OK`).
	    - Requested resource and path.
	- Can filter requests by resource type or keyword.
- #### **Inspecting Requests and Responses**:
	1. Click on a specific request to view details.
	2. Use the **Response Tab** to see the response body.
	3. Click **Raw** to view unrendered source code.



### **6. Key Takeaways**
1. HTTP requests consist of a **method**, **path**, **version**, **headers**, and optionally a **body**.
2. HTTP responses contain a **status code**, **headers**, and optionally a **body**.
3. Tools like **cURL** and **Browser DevTools** are essential for analyzing HTTP communications.
4. Verbose flags (`-v`, `-vvv`) in cURL provide comprehensive details about the request and response.



### Questions
- What is the HTTP method used while intercepting the request? (case-sensitive)
	- GET
- Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)
	- 2.4.41