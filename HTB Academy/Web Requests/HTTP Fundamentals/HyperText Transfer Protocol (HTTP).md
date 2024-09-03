### HTTP Overview

- **HTTP (HyperText Transfer Protocol)**: An application-level protocol used to access World Wide Web resources.
    
- **Components**:
    
    - **Scheme**: Identifies the protocol (e.g., `http://`, `https://`).
    - **User Info**: Optional credentials (e.g., `admin:password@`).
    - **Host**: Resource location (e.g., `inlanefreight.com`).
    - **Port**: Default is port 80 for HTTP, port 443 for HTTPS (e.g., `:80`).
    - **Path**: Points to the specific resource (e.g., `/dashboard.php`).
    - **Query String**: Parameters and values (e.g., `?login=true`).
    - **Fragments**: Client-side sections (e.g., `#status`).
- **HTTP Flow**:
    
    1. **DNS Resolution**: Browser requests IP address for the domain (e.g., `inlanefreight.com`).
    2. **GET Request**: Browser sends a GET request to the HTTP port.
    3. **Response**: Server processes the request, returns the resource (e.g., `index.html`), and a status code (e.g., `200 OK`).
    4. **Rendering**: Browser renders the content for the user.

### cURL

- **cURL (Client URL)**: A command-line tool and library for transferring data with URLs.
    - **Basic Usage**: Send a web request by providing the URL as an argument.
        
        - cURL displays raw HTML/JavaScript/CSS code instead of rendering it like a browser.
    - **Downloading Files**:
        
        - To save content with the remote file name, use the `-O` flag.
        - To save content with a specific file name, use the `-o` flag followed by the desired name.
    - **Silent Mode**: Use the `-s` flag to suppress progress and error messages, saving only the file output.
        
    - **Help Options**: Use the `-h` flag to view available options.
        
        - `-d` or `--data`: Send HTTP POST data.
        - `-i` or `--include`: Include response headers.
        - `-o` or `--output <file>`: Write output to a file.
        - `-O` or `--remote-name`: Save output with the remote file name.
        - `-s` or `--silent`: Silent mode.
        - `-u` or `--user <user:password>`: Provide user credentials.
        - `-A` or `--user-agent <name>`: Set User-Agent string.
        - `-v` or `--verbose`: Enable verbose mode.
    - **Detailed Help**: For more details, use `--help all` for a complete list of options or `man curl` for the full manual.

### Questions
- To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above.
	- HTB{64$!c_cURL_u$3r}