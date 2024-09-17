- **Definition**:
    - A web server is an application that runs on the back-end server. It handles all HTTP traffic from client-side browsers, routes requests to the appropriate pages, and sends responses back to the clients.
- **Port Usage**:
    - **TCP Ports**: Typically operates on TCP ports 80 (HTTP) or 443 (HTTPS).
- **Responsibilities**:
    - Connects end-users to various parts of the web application.
    - Manages responses to client requests, ensuring proper delivery of content.
- **Workflow**:
    - **Receiving Requests**: Accepts HTTP requests from client-side browsers.
    - **Routing Requests**: Routes these requests to the appropriate resources or pages on the web application.
    - **Sending Responses**: Returns HTTP responses to the client-side browser.
        - **HTTP Response Codes**:
            - **200 OK**: Indicates that the request was successful and the server has returned the requested content.
            - **404 NOT FOUND**: Indicates that the requested page or resource could not be found on the server.
            - **403 FORBIDDEN**: Indicates that access to the requested page or resource is restricted or denied.
- **Example**:
    - When a user requests a webpage, the web server processes the request, retrieves the requested content, and responds with the appropriate HTTP response code and content.

![[web-server-requests.jpg]]

**HTTP Response Codes**
- **Successful Responses**:
    - **200 OK**: The request has succeeded.
- **Redirection Messages**:
    - **301 Moved Permanently**: The URL of the requested resource has been changed permanently.
    - **302 Found**: The URL of the requested resource has been changed temporarily.
- **Client Error Responses**:
    - **400 Bad Request**: The server could not understand the request due to invalid syntax.
    - **401 Unauthorized**: Unauthenticated attempt to access a page.
    - **403 Forbidden**: The client does not have access rights to the content.
    - **404 Not Found**: The server cannot find the requested resource.
    - **405 Method Not Allowed**: The request method is known by the server but has been disabled and cannot be used.
    - **408 Request Timeout**: This response is sent on an idle connection by some servers, even without any previous request by the client.
- **Server Error Responses**:
    - **500 Internal Server Error**: The server has encountered a situation it doesn't know how to handle.
    - **502 Bad Gateway**: The server, while working as a gateway to get a response needed to handle the request, received an invalid response.
    - **504 Gateway Timeout**: The server is acting as a gateway and cannot get a response in time.


**Web Server Overview**
- **Function**:
    - Handles HTTP traffic from client-side browsers.
    - Routes requests to the appropriate resources or pages.
    - Responds to client-side browsers with the requested content.
- **Typical Ports**:
    - **Port 80**: For HTTP traffic.
    - **Port 443**: For HTTPS traffic.
- **Request Handling Workflow**:
    - **Receives Requests**: Accepts HTTP requests from client-side browsers.
    - **Routes Requests**: Directs requests to the appropriate resources.
    - **Sends Responses**: Returns HTTP responses and codes based on the request outcome.
- **Example Usage**:
    - **cURL Command for Headers**:
        - `curl -I https://academy.hackthebox.com`
    - **cURL Command for Source Code**:
        - `curl https://academy.hackthebox.com`




**Common Web Server Types**
- **Apache**: 
    - **Description**: Most common web server, hosting over 40% of websites.
    - **Compatibility**: Runs on Linux, Windows, and macOS.
    - **Languages Supported**: PHP, .Net, Python, Perl, Bash (through CGI).
    - **Usage**: Common among startups and smaller companies, used by major companies like Apple, Adobe, and Baidu.
    - **Features**: Open-source, well-maintained, and extensively documented.
- **NGINX**:
    - **Description**: Second most common web server, focusing on high performance with low memory and CPU usage.
    - **Compatibility**: Free and open-source.
    - **Usage**: Popular for high traffic websites, used by Google, Facebook, Twitter, and Netflix.
    - **Features**: Async architecture for efficient handling of concurrent requests.
- **IIS (Internet Information Services)**:
    - **Description**: Third most common web server, developed by Microsoft.
    - **Compatibility**: Runs on Microsoft Windows Servers.
    - **Usage**: Often used with .NET framework, also supports PHP and FTP services.
    - **Features**: Optimized for Active Directory integration, includes Windows Auth for user authentication.
    - **Popular Sites**: Microsoft, Office365, Skype, Stack Overflow, Dell.
- **Other Servers**:
    - **Apache Tomcat**: Used for Java web applications.
    - **Node.js**: For web applications developed using JavaScript on the back end.


## Questions
- If a web server returns an HTTP code 201, what does it stand for?
	- **Created**