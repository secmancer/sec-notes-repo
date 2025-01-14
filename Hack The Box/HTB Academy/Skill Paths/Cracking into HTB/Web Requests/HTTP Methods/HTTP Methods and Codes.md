### **1. HTTP Request Methods**
- HTTP methods specify the action the client wants the server to perform on a resource. 
- Common methods include:

|**Method**|**Description**|
|---|---|
|`GET`|Requests a resource. Additional data can be passed using query strings (e.g., `?param=value`).|
|`POST`|Sends data to the server in the request body. Used for submitting forms, uploading files, etc.|
|`HEAD`|Requests headers only (no body). Useful for checking resource metadata (e.g., size) before downloading.|
|`PUT`|Creates or replaces a resource on the server. Can be dangerous if improperly secured.|
|`DELETE`|Deletes a specified resource on the server. Must be secured to prevent abuse (e.g., DoS attacks).|
|`OPTIONS`|Returns the HTTP methods supported by the server.|
|`PATCH`|Applies partial modifications to an existing resource.|
- #### **Notes**:
	- **Common Usage**:
	    - `GET` and `POST` are the most frequently used methods in modern web applications.
	    - **REST APIs** often utilize `PUT`, `DELETE`, and `PATCH` for managing resources.
	- The server and application configuration determine the availability of specific methods.



### **2. HTTP Response Codes**
- HTTP response codes indicate the status of the client’s request. 
- They are grouped into five categories:

| **Type** | **Description**                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------- |
| `1xx`    | Informational responses, indicating the request is being processed.                             |
| `2xx`    | Success responses, indicating the request was successfully received, understood, and processed. |
| `3xx`    | Redirects, indicating the client must take additional actions to complete the request.          |
| `4xx`    | Client errors, indicating problems with the request (e.g., malformed or unauthorized requests). |
| `5xx`    | Server errors, indicating problems on the server side.                                          |



### **3. Common HTTP Status Codes**

|**Code**|**Description**|
|---|---|
|**`200 OK`**|Indicates a successful request. The response usually contains the requested resource.|
|**`302 Found`**|Redirects the client to another URL. Often used after a successful login.|
|**`400 Bad Request`**|Indicates a malformed request (e.g., syntax errors or missing line terminators).|
|**`403 Forbidden`**|Denies access to a resource due to insufficient permissions or detected malicious input.|
|**`404 Not Found`**|Indicates the requested resource does not exist on the server.|
|**`500 Internal Server Error`**|Indicates a server-side problem preventing the request from being processed.|



### **4. Observing HTTP Methods and Codes**
- #### **Using cURL**:
	- **View HTTP Methods**:
    ```bash
    curl -v http://example.com
    ```
    - The first line of the request shows the method (e.g., `GET / HTTP/1.1`).
- **Change HTTP Method**:
    - Example for `POST`:
        ```bash
        curl -X POST -d "param=value" http://example.com
        ```
- **View Response Codes**:
    - Response codes are included in the headers:
        ```bash
        < HTTP/1.1 200 OK
        ```



#### **Using Browser DevTools**:
1. Open the **Network Tab** ([CTRL+SHIFT+I] or [F12]).
2. Observe the **Method** column for the HTTP method.
3. Check the **Status** column for the response code.



### **5. Key Takeaways**
1. HTTP methods define the type of operation to perform on a resource.
2. Response codes communicate the outcome of the request, whether successful, erroneous, or requiring further actions.
3. Tools like **cURL** and **Browser DevTools** allow detailed analysis of methods and status codes during web interactions.
