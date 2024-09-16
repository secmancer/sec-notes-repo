### Notes: Understanding POST Requests and Their Applications in Web Applications

1. **POST Requests Overview**
    - Web applications use **POST requests** to transfer files or handle sensitive data that shouldn’t appear in the URL.
    - Unlike **GET requests**, which place user parameters in the URL, **POST** embeds parameters in the request body, offering:
        - **Lack of logging**: Large file transfers (e.g., file uploads) are not logged in the URL.
        - **Less encoding requirements**: POST requests handle binary data, requiring minimal encoding.
        - **More data capacity**: URLs have character limits (~2,000 characters), but POST requests can handle larger datasets.
2. **Example: Logging In with POST**
    - A typical **login form** sends a **POST request** with username and password embedded in the body.
    - Example with cURL:
        - Sending credentials:  
            `curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/`
    - To follow redirection after login:  
        `curl -L -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/`
3. **Authenticated Cookies**
    - After successful authentication, web applications usually issue a cookie (e.g., `PHPSESSID`) for session management.
    - cURL can be used to interact with authenticated cookies:
        - View the response and cookies with:
            - `curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/ -i`
        - Use the authenticated cookie:
            - `curl -b 'PHPSESSID=<SESSION_ID>' http://<SERVER_IP>:<PORT>/`
            - Alternatively: `curl -H 'Cookie: PHPSESSID=<SESSION_ID>' http://<SERVER_IP>:<PORT>/`
    - **Setting cookies manually in the browser**:  
        Navigate to the devtools **Storage tab**, replace existing cookie values, and refresh to access the authenticated session.
4. **JSON Data and POST Requests**
    - For functions like **city search**, **POST** requests might send data in **JSON** format.
    - Example POST request with JSON content:
```
curl -X POST -d '{"search":"london"}' \
-b 'PHPSESSID=<SESSION_ID>' \
-H 'Content-Type: application/json' \
http://<SERVER_IP>:<PORT>/search.php
```
- To verify headers and content type, use browser devtools or cURL.
5. **Exercise**
    - Practice sending POST requests with and without cookies or content-type headers to observe how web applications respond differently.
6. **Using Fetch**
    - You can also replicate these requests using **Fetch** in the browser console by copying requests from the devtools (right-click and select **Copy as Fetch**).


## Questions
- Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'
	- HTB{p0$t_r3p34t3r}