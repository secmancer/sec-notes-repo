### Monitoring HTTP Requests and Authentication

#### Exercise: Observing HTTP Requests

1. **Select a Website**: Choose a website to analyze.
2. **Open Browser DevTools**: Open the browser's Developer Tools using `F12` or `Ctrl+Shift+I`.
3. **Navigate to the Network Tab**: This tab shows all network requests made by the page.
4. **Visit the Website**: Watch the Network tab populate with requests as the page loads.
5. **Analyze Requests**: Observe the different HTTP methods used (GET, POST, etc.), URLs, response codes, and content.

This exercise helps you understand how a web application communicates with its backend and can be useful for security assessments or debugging.

#### HTTP Basic Authentication

Basic HTTP authentication is a method for protecting a resource by requiring a username and password. Here’s how to test it with `cURL`:

1. **Accessing Protected Resources**:
    
    - **Initial Request**: Use `curl -i http://<SERVER_IP>:<PORT>/`. The response will include a `401 Authorization Required` status, indicating that basic authentication is required.
    - **Authenticated Request**: Use `curl -u admin:admin http://<SERVER_IP>:<PORT>/`. If the credentials are correct, you will receive the requested page content.
    - **URL with Credentials**: You can also access it using `curl http://admin:admin@<SERVER_IP>:<PORT>/`.
2. **Viewing Response Headers**:
    
    - Add `-i` to your cURL command to see both headers and body: `curl -i -u admin:admin http://<SERVER_IP>:<PORT>/`.
3. **Authorization Header**:
    
    - Use `-v` with cURL to reveal the `Authorization` header: `curl -v -u admin:admin http://<SERVER_IP>:<PORT>/`. The header will show the base64-encoded credentials.
    - **Manually Setting Authorization Header**: Use `curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/`.

#### Using GET Parameters

1. **Search Function**:
    
    - Enter a search term to trigger a GET request to `search.php` with the `search` parameter.
    - **Example Request**: Use `curl 'http://<SERVER_IP>:<PORT>/search.php?search=le' -H 'Authorization: Basic YWRtaW46YWRtaW4='`.
2. **Copying cURL Commands**:
    
    - In the Network tab, right-click the request and select `Copy > Copy as cURL`. Paste and execute this command in your terminal.
3. **Using Fetch**:
    
    - In the Network tab, right-click the request and select `Copy > Copy as Fetch`. Paste this Fetch command into the JavaScript console to execute it.


### Questions
- The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is the request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.
	- HTB{curl_g3773r}