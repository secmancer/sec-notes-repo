### HTTP Headers Overview
- HTTP headers pass information between the client and server.
- Headers can belong to either requests, responses, or both (general headers).
- Headers are divided into categories:
    - General Headers
    - Entity Headers
    - Request Headers
    - Response Headers
    - Security Headers

### General Headers
- Used in both requests and responses, they describe the message itself.
- **Date**: Indicates when the message originated.
    - Example: `Date: Wed, 16 Feb 2022 10:38:44 GMT`
- **Connection**: Controls whether the connection stays open or is closed after the request.
    - Example: `Connection: close`

### Entity Headers
- Describe the content being transferred.
- Common in responses, POST, and PUT requests.
- **Content-Type**: Describes the media type of the resource.
    - Example: `Content-Type: text/html`
- **Content-Length**: Specifies the size of the content.
    - Example: `Content-Length: 385`
- **Content-Encoding**: Specifies encoding transformations applied to the data.
    - Example: `Content-Encoding: gzip`

### Request Headers
- Sent by the client in HTTP requests.
- **Host**: Specifies the domain or IP address being queried.
    - Example: `Host: www.inlanefreight.com`
- **User-Agent**: Provides information about the client (browser, version, OS).
    - Example: `User-Agent: curl/7.77.0`
- **Accept**: Defines the media types the client can handle.
    - Example: `Accept: */*`
- **Authorization**: Contains client authentication data.
    - Example: `Authorization: BASIC cGFzc3dvcmQK`

### Response Headers
- Sent by the server in HTTP responses.
- **Server**: Provides details about the server handling the request.
    - Example: `Server: Apache/2.2.14 (Win32)`
- **Set-Cookie**: Sends cookies from the server to the client.
    - Example: `Set-Cookie: PHPSESSID=b4e4fbd93540`
- **WWW-Authenticate**: Specifies the authentication method required.
    - Example: `WWW-Authenticate: BASIC realm="localhost"`

### Security Headers
- Enhance security by specifying browser behaviors.
- **Content-Security-Policy**: Controls which external resources are allowed.
    - Example: `Content-Security-Policy: script-src 'self'`
- **Strict-Transport-Security**: Forces HTTPS usage for all communication.
    - Example: `Strict-Transport-Security: max-age=31536000`

### cURL
- The `-v` flag shows complete request and response details.
- The `-I` flag sends a `HEAD` request and displays only response headers.
- The `-i` flag shows both headers and the response body.
- Example:
    - `curl -I https://www.inlanefreight.com`
    - Output shows headers like `Date`, `Content-Length`, `Content-Type`, etc.

### Browser DevTools
- HTTP headers can be inspected in the "Network" tab of browser developer tools.
- Headers are displayed in both raw and formatted views. Cookies are shown in a separate tab.

### Exercises
1. Review HTTP headers and recall their usage.
2. Use cURL’s `-I` or `-v` flag to change the `User-Agent` with the `-A` option.
3. Practice previewing HTTP headers via browser devtools.


## Questions
- The server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.
	- HTB{p493_r3qu3$t$_m0n!t0r}