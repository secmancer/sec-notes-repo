### Notes on HTTP Communications

1. **HTTP Requests and Responses**
    - **HTTP Request** is made by the client (browser/cURL) and processed by the server (web server).
    - Contains details such as resource (URL, path, parameters), request data, headers, and options.
    - **HTTP Response** is sent back by the server containing a response code and resource data (if accessible).
2. **HTTP Request Structure**
    - Example: `GET http://inlanefreight.com/users/login.html`
    - Consists of three fields:
        - **Method**: Type of action to perform (e.g., GET, POST).
        - **Path**: Resource being accessed (e.g., `/users/login.html`).
        - **Version**: HTTP version used (e.g., HTTP/1.1).
    - Followed by headers like `Host`, `User-Agent`, `Cookie`.
    - Ends with request body/data (if applicable).
3. **HTTP Response Structure**
    - Example: `HTTP/1.1 200 OK`
    - Contains:
        - HTTP version.
        - Response code indicating the status.
    - Response headers (e.g., Date, Content-Type).
    - Response body (e.g., HTML, JSON, images, documents).
4. **HTTP Version Differences**
    
    - **HTTP 1.X**: Sends requests as clear-text, separating fields and requests using new-line characters.
    - **HTTP 2.X**: Sends requests as binary data in a dictionary form.
5. **Using cURL**
    - cURL can show full HTTP requests and responses using the `-v` flag (verbose output).
    - Example command:
        - `curl inlanefreight.com -v`
        - Shows request headers (`GET /`, `Host`, `User-Agent`) and response headers (`HTTP/1.1 401 Unauthorized`, `Content-Type`).
    - **-vvv** flag provides even more detailed information.
6. **Browser Developer Tools (DevTools)**
    - Accessible via `CTRL+SHIFT+I` or `F12` in Chrome/Firefox.
    - **Network Tab**: Shows web requests, methods (e.g., GET), response status, and requested URLs/paths.
    - Useful for monitoring web requests during penetration tests or web assessments.
7. **Exercise**
    - Use the `-vvv` flag in cURL to explore extra details in requests and responses.
    - Explore DevTools in the browser to filter and assess specific network requests.


## Questions
- What is the HTTP method used while intercepting the request? (case-sensitive)
	- GET
- Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)
	- 2.4.41