### POST Requests Overview
- In contrast to GET requests, POST requests are used when web applications need to send data that may be too large to include in the URL or when security is a concern. POST requests encapsulate data within the HTTP request body rather than the URL. 
- This is more efficient for large or sensitive data and allows more data to be transmitted compared to GET requests, which are limited by URL length constraints.



### Key Benefits of POST Requests:
- **No Logging of Sensitive Data**: POST requests transfer data within the request body, meaning sensitive data (e.g., passwords or files) doesn't get logged as part of the URL.
- **Handling Binary Data**: POST can send binary data, which would be problematic in a GET request due to URL encoding limitations.
- **Larger Payloads**: Unlike GET requests, which are restricted to a certain URL length (typically around 2,000 characters), POST can handle much larger data payloads.



### Practical Example: Login Form with POST
- When interacting with a login form, the credentials are usually sent via a POST request. For instance, when logging into a PHP-based web application, the username and password are typically sent as POST parameters like:
```
username=admin&password=admin
```
#### Example cURL Command to Send a POST Request:
```bash
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/
```
- This will authenticate the user, and if successful, the web application will typically return a response that either redirects to another page or shows the authenticated content.



- ### Authentication with Cookies
- After a successful login, many web applications send a session cookie (e.g., `PHPSESSID`) to the client, allowing the user to stay authenticated on subsequent requests.
- To test this, we can view the response headers and extract the cookie, which can then be reused in future requests with the `-b` flag in cURL:
```bash
curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/
```
- This allows us to interact with the application without needing to re-enter credentials.



### Sending JSON Data with POST
- Some web applications may use JSON data in POST requests. 
- For example, when interacting with a city search function, the POST request may look like this:
```json
{"search":"london"}
```
- We need to ensure the `Content-Type` is set to `application/json`, which can be done in cURL using the `-H` flag:
```bash
curl -X POST -d '{"search":"london"}' -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' -H 'Content-Type: application/json' http://<SERVER_IP>:<PORT>/search.php
```
- This request returns a JSON response with matching cities, such as `["London (UK)"]`.



### Using Fetch in the Browser
- Instead of using cURL, the same POST request can be made from the browser's developer console using the `fetch()` function. 
- By copying the request as a Fetch command from the devtools, we can execute it directly in the console:
```javascript
fetch('http://<SERVER_IP>:<PORT>/search.php', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Cookie': 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1'
  },
  body: JSON.stringify({ search: 'london' })
})
  .then(response => response.json())
  .then(data => console.log(data));
```
- This allows us to perform requests directly from the browser, bypassing the need for a front-end form.



### Key Takeaways:
- POST requests are essential for sending sensitive or large data, including file uploads and form submissions.
- Authentication can be managed using cookies, which persist across multiple requests.
- JSON data is commonly used in modern web applications, and POST requests can easily handle this with the correct headers.
- Tools like cURL and the browser's developer tools (or Fetch API) are valuable for testing and interacting with web applications in security assessments.



### Questions
- Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'
	- HTB{p0$t_r3p34t3r}