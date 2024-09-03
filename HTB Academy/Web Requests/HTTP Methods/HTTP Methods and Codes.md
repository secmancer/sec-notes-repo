### HTTP Request Methods

HTTP supports various methods to interact with resources on a server. Here are some commonly used methods:

- **GET**: Requests a specific resource. Data can be sent as query strings (e.g., `?param=value`). This method retrieves information without modifying the resource.
    
- **POST**: Sends data to the server in the request body. This is used for submitting forms, uploading files, or sending other types of data. The data is included after the headers in the request body.
    
- **HEAD**: Requests only the headers of a resource. It is useful for checking meta-information (e.g., response length) without downloading the full resource.
    
- **PUT**: Updates or creates a resource at a specified location. It sends data in the request body to update the resource.
    
- **DELETE**: Removes a resource from the server. It requires careful security measures to prevent accidental deletion of important resources.
    
- **OPTIONS**: Provides information about the communication options available for a resource, such as the allowed HTTP methods.
    
- **PATCH**: Applies partial modifications to a resource. Unlike PUT, which replaces the entire resource, PATCH updates only the specified parts.
    

### HTTP Response Codes

HTTP response codes inform the client about the status of their request. They are categorized as follows:

#### 1xx (Informational)

- **100 Continue**: Indicates that the initial part of the request was received and the client should continue with the request.

#### 2xx (Successful)

- **200 OK**: The request succeeded, and the response contains the requested resource.
- **201 Created**: The request was successful, and a new resource was created.
- **204 No Content**: The request was successful, but there is no content to return.

#### 3xx (Redirection)

- **301 Moved Permanently**: The resource has been permanently moved to a new URL.
- **302 Found**: The resource has temporarily moved to a different URL. The client should use the URL provided in the `Location` header.

#### 4xx (Client Error)

- **400 Bad Request**: The server could not understand the request due to malformed syntax.
- **401 Unauthorized**: Authentication is required to access the resource.
- **403 Forbidden**: The server understands the request but refuses to authorize it.
- **404 Not Found**: The requested resource could not be found on the server.

#### 5xx (Server Error)

- **500 Internal Server Error**: The server encountered an unexpected condition that prevented it from fulfilling the request.
- **502 Bad Gateway**: The server received an invalid response from an upstream server while trying to fulfill the request.
- **503 Service Unavailable**: The server is currently unable to handle the request due to maintenance or overload.

### Using cURL

- **Display Request and Response**:
    
    - Use `-v` to view detailed information including the HTTP method and response codes.
- **Show Response Headers Only**:
    
    - Use `-I` to send a HEAD request and display only the response headers.
- **Show Both Headers and Body**:
    
    - Use `-i` to display both the headers and the response body.

### Browser DevTools

- **Network Tab**:
    
    - Open the DevTools and navigate to the Network tab to view HTTP requests and responses.
    - The Method column shows the HTTP method used for each request.
- **Headers Tab**:
    
    - Displays both request and response headers. You can view these in raw format by clicking the Raw button.