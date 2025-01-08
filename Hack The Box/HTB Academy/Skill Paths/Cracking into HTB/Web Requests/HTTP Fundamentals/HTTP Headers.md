### Notes on HTTP Headers

---

### **1. Overview of HTTP Headers**

- HTTP headers provide additional metadata about a request or response.
- Headers are categorized as:
    1. **General Headers**: Contextual, describing the message itself.
    2. **Entity Headers**: Describe the content (entity) being transferred.
    3. **Request Headers**: Sent by the client to provide additional context or data.
    4. **Response Headers**: Sent by the server to provide additional response information.
    5. **Security Headers**: Enhance security by enforcing policies.

---

### **2. Categories of Headers**

#### **a. General Headers**

|**Header**|**Example**|**Description**|
|---|---|---|
|`Date`|`Date: Wed, 16 Feb 2022 10:38:44 GMT`|Specifies the timestamp when the message originated. Preferred format: UTC time zone.|
|`Connection`|`Connection: keep-alive`|Determines if the connection remains open (`keep-alive`) or closes (`close`) after the request.|

---

#### **b. Entity Headers**

|**Header**|**Example**|**Description**|
|---|---|---|
|`Content-Type`|`Content-Type: text/html`|Specifies the type of resource being transferred (e.g., `text/html`, `application/json`).|
|`Media-Type`|`Media-Type: application/pdf`|Describes the data format, often paired with `charset` for encoding (e.g., `UTF-8`).|
|`Boundary`|`boundary="b4e4fbd93540"`|Separates content within a message, useful for multipart/form-data.|
|`Content-Length`|`Content-Length: 385`|Specifies the size of the message body in bytes. Automatically set by browsers and tools.|
|`Content-Encoding`|`Content-Encoding: gzip`|Indicates transformations (e.g., compression) applied to the message.|

---

#### **c. Request Headers**

|**Header**|**Example**|**Description**|
|---|---|---|
|`Host`|`Host: www.example.com`|Identifies the target server. Used to resolve multi-host configurations.|
|`User-Agent`|`User-Agent: curl/7.77.0`|Specifies the client making the request (e.g., browser or tool).|
|`Referer`|`Referer: https://google.com`|Indicates the URL of the previous page that led to the current request.|
|`Accept`|`Accept: */*`|Lists the content types the client accepts (e.g., `application/json`, `text/html`).|
|`Cookie`|`Cookie: PHPSESSID=b4e4fbd93540`|Contains session identifiers or preferences sent from client to server.|
|`Authorization`|`Authorization: BASIC cGFzc3dvcmQK`|Provides credentials (e.g., tokens) for authenticated requests.|

---

#### **d. Response Headers**

|**Header**|**Example**|**Description**|
|---|---|---|
|`Server`|`Server: Apache/2.4.41`|Provides information about the server software.|
|`Set-Cookie`|`Set-Cookie: PHPSESSID=abc123`|Used to define cookies for the client.|
|`WWW-Authenticate`|`WWW-Authenticate: Basic realm="Login"`|Specifies the type of authentication required (e.g., Basic, Bearer).|

---

#### **e. Security Headers**

|**Header**|**Example**|**Description**|
|---|---|---|
|`Content-Security-Policy`|`script-src 'self'`|Restricts allowed sources for scripts to prevent XSS attacks.|
|`Strict-Transport-Security`|`max-age=31536000`|Forces HTTPS communication, preventing plaintext HTTP traffic.|
|`Referrer-Policy`|`Referrer-Policy: origin`|Controls what information is included in the `Referer` header to avoid leaking sensitive data.|

---

### **3. Viewing and Modifying Headers with cURL**

- **View Response Headers Only**:
    
    ```bash
    curl -I https://example.com
    ```
    
    - Sends a `HEAD` request and displays response headers.
- **View Both Headers and Body**:
    
    ```bash
    curl -i https://example.com
    ```
    
- **Modify Headers**:
    
    - Use `-H` to set custom headers:
        
        ```bash
        curl -H "Authorization: Bearer token123" https://example.com
        ```
        
- **Set User-Agent**:
    
    ```bash
    curl -A "Mozilla/5.0" https://example.com
    ```
    

---

### **4. Inspecting Headers with Browser DevTools**

1. Open DevTools:
    - **Windows/Linux**: `[CTRL+SHIFT+I]` or `[F12]`.
    - **Mac**: `[CMD+OPT+I]`.
2. Go to the **Network Tab**.
3. Click on a request to view its details:
    - **Headers Tab**: Displays request and response headers.
    - **Cookies Tab**: Shows cookies used in the request.
    - **Raw Button**: Displays raw header format.

---

### **5. Key Takeaways**

- HTTP headers provide essential metadata for requests and responses.
- Headers are grouped into general, entity, request, response, and security categories.
- Tools like **cURL** and **DevTools** allow detailed inspection and modification of headers for analysis and testing.



### Questions
- The server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.
	- HTB{p493_r3qu3$t$_m0n!t0r}