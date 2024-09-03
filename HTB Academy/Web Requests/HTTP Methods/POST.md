### POST Requests Overview

POST requests are used for transferring data to a server, especially when dealing with forms or file uploads. Unlike GET requests, which append data to the URL, POST requests include data in the request body. This method offers several advantages:

- **Lack of Logging**: POST requests are better suited for large data transfers (like file uploads) as they do not include data in the URL, avoiding extensive logging.
- **Less Encoding Requirements**: POST requests can handle binary data and special characters, which are not constrained by URL encoding.
- **More Data**: POST requests can handle larger amounts of data compared to GET requests, which are limited by URL length constraints.

### Login Forms

To demonstrate POST requests, let's work with a login form:

1. **Login Attempt**:
    
    - When you log in with credentials like `admin:admin`, you send a POST request to authenticate.
    - In the Network tab of your browser DevTools, after logging in, you’ll see POST requests with data such as `username=admin&password=admin`.
2. **Using cURL**:
    
    - To replicate this POST request using cURL, use: `curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/`
    - If redirection occurs after login, use `-L` to follow it: `curl -X POST -d 'username=admin&password=admin' -L http://<SERVER_IP>:<PORT>/`
3. **Authenticated Cookies**:
    
    - On successful login, you'll receive a cookie (e.g., `PHPSESSID`).
    - View the response with: `curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/ -i`
    - Use the cookie to make authenticated requests: `curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/`
    - You can also set the cookie as a header: `curl -H 'Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/`
4. **Using Browser DevTools**:
    
    - Log in, then check the Storage tab in DevTools (`SHIFT+F9`) to see and manage cookies.
    - Set or replace cookies as needed to test authenticated sessions.

### JSON Data

1. **Sending JSON Data**:
    
    - For search functionalities using JSON data, observe requests in the Network tab.
    - Example POST request: `curl -X POST -d '{"search":"london"}' -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' -H 'Content-Type: application/json' http://<SERVER_IP>:<PORT>/search.php`
    - Ensure you include `Content-Type: application/json` header.
2. **Testing with Fetch**:
    
    - Copy the request as Fetch from DevTools and execute in the Console tab: `fetch('http://<SERVER_IP>:<PORT>/search.php', { method: 'POST', headers: { 'Content-Type': 'application/json', 'Cookie': 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' }, body: JSON.stringify({ search: 'london' }) }).then(response => response.json()).then(data => console.log(data));`

### Questions
- Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'
	- HTB{p0$t_r3p34t3r}