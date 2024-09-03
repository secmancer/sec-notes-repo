### HTTP Headers Categories

#### General Headers

- **Date**: Indicates the date and time when the message was sent. It is generally preferred to use UTC.
- **Connection**: Determines whether the connection should remain open or be closed after the request. Common values are `close` and `keep-alive`.

#### Entity Headers

- **Content-Type**: Describes the type of content being sent (e.g., `text/html`). It may also include the character encoding (e.g., `charset=UTF-8`).
- **Media-Type**: Similar to `Content-Type`, specifying the type of data (e.g., `application/pdf`).
- **Boundary**: Used to separate different parts of a multipart message (e.g., in form submissions).
- **Content-Length**: Specifies the size of the content in the message body.
- **Content-Encoding**: Indicates the encoding applied to the content (e.g., `gzip`).

#### Request Headers

- **Host**: Specifies the domain name of the server (e.g., `www.inlanefreight.com`).
- **User-Agent**: Provides information about the client making the request (e.g., browser type and version).
- **Referer**: Indicates the URL from which the request originated.
- **Accept**: Lists the media types that the client is willing to receive (e.g., `*/*`).
- **Cookie**: Contains cookies sent to the server (e.g., `PHPSESSID=b4e4fbd93540`).
- **Authorization**: Used for client authentication, providing tokens or credentials (e.g., `BASIC cGFzc3dvcmQK`).

#### Response Headers

- **Server**: Provides information about the server software handling the request (e.g., `Apache/2.2.14`).
- **Set-Cookie**: Contains cookies that the server wants the client to store (e.g., `PHPSESSID=b4e4fbd93540`).
- **WWW-Authenticate**: Indicates the authentication method required by the server.

#### Security Headers

- **Content-Security-Policy**: Defines policies for allowed sources of content to prevent security threats like XSS (e.g., `script-src 'self'`).
- **Strict-Transport-Security**: Enforces the use of HTTPS and prevents communication over HTTP (e.g., `max-age=31536000`).
- **Referrer-Policy**: Controls the amount of referrer information sent with requests (e.g., `origin`).

### Using cURL

- **View Headers Only**:
    
    - Use the `-I` flag to send a HEAD request and view only response headers.
- **View Both Headers and Body**:
    
    - Use the `-i` flag to display both headers and the response body.
- **Example**:
    
    - `curl -I https://www.inlanefreight.com` shows response headers only.
    - `curl https://www.inlanefreight.com -A 'Mozilla/5.0'` changes the User-Agent header.

### Browser DevTools

- **Network Tab**:
    
    - Open DevTools (e.g., `CTRL+SHIFT+I` or `F12`) and navigate to the Network tab to view requests and responses.
    - Click on a request to see its details, including headers.
- **Headers Tab**:
    
    - Shows both request and response headers. You can view them in raw format by clicking the Raw button.
    - The Cookies tab provides information on cookies used by the request.

### Questions:
- The server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.
	- HTB{p493_r3qu3$t$_m0n!t0r}