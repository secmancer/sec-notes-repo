### **GET Request:**
- **Definition:** A GET request is sent by the browser when accessing a URL to retrieve resources hosted at that address.
- **Observation:** The Network tab in the browser devtools can be used to monitor GET requests, allowing us to see how the page interacts with the backend.
- **Exercise:** To understand web application behavior, visit any website and monitor the Network tab to observe how it performs requests. This is useful for web application assessments or bug bounty exercises.



### **HTTP Basic Authentication:**
- **Mechanism:** Unlike standard login forms (which use POST requests), Basic Authentication is handled directly by the web server. This method is used to protect specific pages or directories.
    - After entering valid credentials (e.g., `admin:admin`), the page becomes accessible.
- **Example using cURL:**
    ```bash
    curl -i http://<SERVER_IP>:<PORT>/
    ```
    - If authentication is required, the response will indicate an error (e.g., `401 Unauthorized`), and the `WWW-Authenticate` header will contain the authentication type (e.g., `Basic realm="Access denied"`).
- **Accessing Authenticated Pages with cURL:**
    - Use the `-u` flag to provide credentials.
        ```bash
        curl -u admin:admin http://<SERVER_IP>:<PORT>/
        ```
- **Alternative Method:**
    - Basic HTTP auth can also be provided directly in the URL: `http://admin:admin@<SERVER_IP>:<PORT>/`.
- **Exercise:** Try adding `-i` to cURL requests to view response headers and compare authenticated versus unauthenticated responses.



### **HTTP Authorization Header:**
- **Encoded Credentials:** The credentials are base64-encoded and appear in the `Authorization` header as `Basic YWRtaW46YWRtaW4=`, which corresponds to `admin:admin`.
- **Manual Header Setting with cURL:** You can also manually set the `Authorization` header to authenticate a request:
    ```bash
    curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/
    ```
 



### **GET Parameters:**
- **Usage in Search Functionality:** In a web application, GET parameters are often used to pass data, such as search terms. For example, a search request might look like:    
    ```http
    GET /search.php?search=le
    ```
- **Observing Requests in Browser Devtools:** When interacting with a search function, you can observe requests in the Network tab. The search query is passed as a GET parameter (e.g., `search=le`).
- **Exercise:** Monitor the Network tab while performing a search. You may notice a GET request to a PHP file (e.g., `search.php`) containing search parameters.
- **Using cURL to Simulate GET Requests:** You can use cURL to replicate GET requests with parameters:
    ```bash
    curl 'http://<SERVER_IP>:<PORT>/search.php?search=le' -H 'Authorization: Basic YWRtaW46YWRtaW4='
    ```
    - The response will typically be the search results in a specific format (e.g., HTML, JSON).
- **Copying cURL Requests:** From the browser devtools, right-click a request and select `Copy > Copy as cURL` to get the exact cURL command, including headers.
- **Using JavaScript Fetch API:** Alternatively, you can copy a request as a Fetch command and execute it in the browser's JavaScript console:    
    ```javascript
    fetch('http://<SERVER_IP>:<PORT>/search.php?search=le', { method: 'GET', headers: { 'Authorization': 'Basic YWRtaW46YWRtaW4=' } })
    ```



### Questions
 - The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is the request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.
	 - HTB{curl_g3773r}