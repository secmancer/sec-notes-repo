### HTTP Requests

- **Structure**:
    
    - **Request Line**:
        
        - **Method**: Indicates the action to perform (e.g., GET).
        - **Path**: The resource being accessed (e.g., `/users/login.html`).
        - **Version**: HTTP version (e.g., `HTTP/1.1`).
    - **Headers**: Key-value pairs that provide additional details about the request (e.g., `Host`, `User-Agent`, `Cookie`). Each header ends with a new line.
        
    - **Body**: Optional. Contains data sent with the request (e.g., form data).
        
- **Note**: HTTP/1.X sends requests as clear-text with new-line characters separating fields, while HTTP/2.X uses binary data.
    

### HTTP Responses

- **Structure**:
    - **Status Line**:
        
        - **Version**: HTTP version (e.g., `HTTP/1.1`).
        - **Status Code**: Response code and message (e.g., `200 OK`).
    - **Headers**: Key-value pairs that provide details about the response (e.g., `Date`, `Content-Length`, `Content-Type`).
        
    - **Body**: Optional. Contains the resource data or error message. It can include HTML, JSON, images, etc.
        

### cURL for HTTP Requests and Responses

- **Basic Usage**:
    
    - To view the HTTP request and response, add the `-v` (verbose) flag to your cURL command.
- **Detailed Output**:
    
    - For more detailed output, use the `-vvv` flag with cURL.

### Browser DevTools

- **Access**:
    
    - Open DevTools in Chrome or Firefox using `CTRL+SHIFT+I` or `F12`.
- **Network Tab**:
    
    - **Purpose**: Displays all network requests and responses.
    - **Usage**:
        - Refresh the page to view the list of requests.
        - Check details such as response status, request method, URL, and path.
        - Use filters to locate specific requests if there are many.

### Questions
- What is the HTTP method used while intercepting the request? (case-sensitive)
	- GET
- Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)
	- 2.4.41