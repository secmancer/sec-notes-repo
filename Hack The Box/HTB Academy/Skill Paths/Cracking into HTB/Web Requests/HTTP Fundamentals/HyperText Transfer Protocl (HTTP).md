### **1. HTTP Basics**
- **Definition**:
    - HTTP is an application-level protocol used for accessing resources on the World Wide Web.
    - Operates in a **client-server model**, where the client sends requests, and the server processes and responds.
- **Default Port**:
    - **HTTP**: Port **80**.
    - **HTTPS**: Port **443**.
- #### **Key Components of HTTP Communication**:
	1. **Client**:
	    - Sends requests (e.g., browser or tools like cURL).
	2. **Server**:
	    - Processes requests and returns resources or status codes.



### **2. URL Structure**
- Resources on the web are accessed via URLs. Each URL has specific components:
    |**Component**|**Example**|**Description**|
    |---|---|---|
    |**Scheme**|`http://` or `https://`|Protocol used for communication. Ends with `://`.|
    |**User Info**|`admin:password@`|(Optional) Credentials for authentication, separated by `:` and ending with `@`.|
    |**Host**|`example.com`|Location of the resource, e.g., domain or IP address.|
    |**Port**|`:80`|(Optional) Specifies the port number. Defaults: 80 (HTTP), 443 (HTTPS).|
    |**Path**|`/index.html`|Specifies the resource on the server (e.g., a file or directory).|
    |**Query**|`?key=value`|(Optional) Key-value pairs for parameters. Multiple parameters separated by `&`.|
    |**Fragment**|`#section`|(Optional) Client-side reference, typically used for navigating within a page.|
- #### **Mandatory Components**:
	- **Scheme** and **Host** are required to locate the resource.



### **3. HTTP Request Flow**
1. **Domain Resolution**:
    - The browser sends a request to a DNS server to resolve the domain name (e.g., `example.com`) to an IP address.
    - DNS lookup checks `/etc/hosts` locally first before querying external DNS servers.
2. **Request**:
    - A GET request is sent to the resolved IP address, typically on port 80, targeting `/` (root).
    - The server processes the request and sends a response.
3. **Response**:
    - Server returns an HTML file (e.g., `index.html`) with a status code.
    - The browser renders the response content.
- #### **Common HTTP Status Codes**:
	- **200 OK**: Request processed successfully.
	- **404 Not Found**: Requested resource does not exist.
	- **500 Internal Server Error**: Server encountered an error.



### **4. Using cURL for HTTP Requests**
- **What is cURL?**
    - A command-line tool to send web requests and retrieve responses.
    - Supports automation and scripting for penetration testing.
- #### **Basic Commands**:
	1. **Send a Basic Request**:
    ```bash
    curl http://example.com
    ```
    - Fetches and prints the raw HTML content of the resource.
2. **Download a File**:
    - **Save with Remote Filename**:
        ```bash
        curl -O http://example.com/index.html
        ```
    - **Save with Custom Filename**:
        ```bash
        curl -o custom_name.html http://example.com/index.html
        ```
3. **Silent Mode**:
    - Suppress output (e.g., progress information):
        ```bash
        curl -s -O http://example.com/index.html
        ```
4. **List Available Flags**:
    ```bash
    curl -h
    ```
    - Example Flags:
        |**Flag**|**Description**|
        |---|---|
        |`-d`|Add POST data.|
        |`-i`|Include HTTP response headers.|
        |`-u`|Specify username and password for authentication.|
        |`-A`|Set custom User-Agent string.|
        |`-v`|Enable verbose output.|
5. **Detailed Documentation**:
    - Use `man curl` or `curl --help all` to access a complete list of commands and options.



### **Key Takeaways**
1. HTTP facilitates communication between clients and servers, enabling access to web resources.
2. A URL provides a structured way to locate resources, with optional components for more specificity.
3. Tools like cURL are essential for penetration testers to send and analyze HTTP requests efficiently.
4. Mastering cURL commands and flags enhances the ability to automate testing and interact with web resources.



### Questions
- To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above.
	- HTB{64$!c_cURL_u$3r}