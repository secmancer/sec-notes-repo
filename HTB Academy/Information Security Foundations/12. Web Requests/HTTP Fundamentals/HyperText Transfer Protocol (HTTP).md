**HTTP Overview**
- Most applications today (web and mobile) interact with the internet using **HTTP** (Hypertext Transfer Protocol).
- HTTP is an **application-level protocol** designed for accessing resources on the **World Wide Web**.
- **Client-server model**: Clients send requests to servers, which process the requests and return resources.
- Default port for HTTP communication is **port 80**, though this can be changed depending on the server configuration.
- When accessing websites, users enter a **Fully Qualified Domain Name (FQDN)** in the form of a **URL** (Uniform Resource Locator).

**URL Structure**
- A URL provides specifications beyond just the website address. It has the following components:
    - **Scheme**: Defines the protocol (e.g., `http://`, `https://`).
    - **User Info**: Optional credentials for authentication (e.g., `admin:password@`).
    - **Host**: The location of the resource (e.g., `inlanefreight.com`).
    - **Port**: The port number (default for `http` is **80**, `https` is **443**).
    - **Path**: Resource being accessed (e.g., `/dashboard.php`).
    - **Query String**: Parameters and values (e.g., `?login=true`).
    - **Fragment**: Client-side identifiers to locate sections within a resource (e.g., `#status`).

**HTTP Flow**
- When a user enters a URL, the browser sends a request to a **DNS server** to resolve the domain into an IP address.
    - If not found locally in the `/etc/hosts` file, the DNS server resolves the domain.
    - The browser sends a **GET request** to the web server at the resolved IP and default port.
- The web server processes the request and returns an **HTTP response** containing the resource (e.g., `index.html`) and a **status code** (e.g., `200 OK`).
- The browser then renders the content for the user.

**cURL Basics**
- **cURL** (Client URL) is a command-line tool used to make HTTP requests and supports multiple protocols.
- Useful for **web penetration testing** and sending requests without needing a web browser.

**Common cURL Commands**
- Send a simple HTTP request:
    - `curl inlanefreight.com`
- Download a file using `-O` to save with the same name as on the server:
    - `curl -O inlanefreight.com/index.html`
- Download and specify a custom file name with `-o`:
    - `curl -o custom_name.html inlanefreight.com/index.html`
- Silent mode (`-s`) to suppress output:
    - `curl -s -O inlanefreight.com/index.html`
- Use the help menu to view available options:
    - `curl -h`
    - `man curl` for detailed documentation.

**cURL Common Flags**
- `-d`: Send **POST** data.
- `-i`: Include **response headers** in the output.
- `-o`: Write output to a **file**.
- `-O`: Use the **remote file name** for output.
- `-s`: **Silent** mode.
- `-u`: Provide **user credentials** for authentication.
- `-A`: Specify a **User-Agent** for the request.
- `-v`: Enable **verbose** mode.

These are foundational elements to understand the HTTP protocol and utilize cURL for efficient web penetration testing and automation.


## Questions
- To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above.
	- HTB{64$!c_cURL_u$3r}