### Notes on HTTP Requests and Authentication:

1. **Default GET Requests**:
    - Browsers send a **GET** request when visiting any URL to obtain resources hosted at that URL.
    - Additional requests using various HTTP methods may be sent after the initial page load, which can be observed via the **Network tab** in browser devtools.
2. **Exercise**:
    - Monitor the **Network tab** in browser devtools when visiting any website to observe how the web application interacts with its backend. This is useful for web assessments and bug bounty exercises.
3. **HTTP Basic Auth**:
    - Basic HTTP authentication involves the browser or cURL providing a **username** and **password** to the web server, which is handled by the server without needing a web application login form.
    - Credentials are sent in the format `username:password`, and browsers or cURL handle encoding this in base64 to the `Authorization` header.
    - Example with cURL:
        - Unauthenticated request:
```
curl -i http://<SERVER_IP>:<PORT>/
```
- Response shows `WWW-Authenticate: Basic realm="Access denied"`.
- Authenticated request:
```
curl -u admin:admin http://<SERVER_IP>:<PORT>/
```
- Alternatively, credentials can be passed directly in the URL:
```
curl http://admin:admin@<SERVER_IP>:<PORT>/
```


4. **Authorization Header**:
- The `Authorization` header contains the base64 encoded credentials for basic auth.
- Example setting the `Authorization` header manually:
```
curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/
```
- You can inspect HTTP requests and responses by using the `-v` flag in cURL to view details like headers.


5. **GET Parameters**:
- Some web applications use **GET parameters** to pass data, as seen in search queries.
- Example:
    - A search query might send a request to `search.php?search=le` to retrieve results.
    - This can be replicated using cURL:
```
curl 'http://<SERVER_IP>:<PORT>/search.php?search=le' -H 'Authorization: Basic YWRtaW46YWRtaW4='
```
- Browser devtools allow copying the HTTP request as a cURL or **Fetch** command, which can be executed in the terminal or JavaScript console for testing.


6. **Inspecting Requests in Browser Devtools**:
- Use browser devtools to:
    - Clear previous requests (via the trash icon) before making a new one.
    - Right-click on requests to **Copy as cURL** or **Copy as Fetch** to replicate the request.
    - View response details, expand data, and analyze results.


## Questions
- The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is the request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.
	- HTB{curl_g3773r}