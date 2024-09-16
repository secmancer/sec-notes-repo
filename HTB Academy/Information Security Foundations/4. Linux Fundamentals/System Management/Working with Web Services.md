**Web Servers on Linux:**
- **Apache** is a widely used web server that supports various functionalities:
    - **mod_ssl**: Encrypts communication between browser and web server.
    - **mod_proxy**: Allows Apache to function as a proxy server.
    - **mod_headers**: Performs complex manipulations of HTTP header data.
    - **mod_rewrite**: Allows URL rewriting.

**Installation of Apache:** To install Apache on a Linux system, use the following command:
```
apt install apache2 -y
```
- This installs the Apache web server.
- After installation, you can check if it's running by navigating to [http://localhost](http://localhost) in your browser, which should display the default Apache page.


**cURL:**
- **cURL** is a tool for transferring files and testing websites over various protocols (HTTP, HTTPS, FTP, etc.).
- Example command to view content from a web server:
```
curl http://localhost
```


**Wget:**
- **wget** is an alternative to cURL for downloading files from FTP or HTTP servers directly from the terminal.
- Example command to download content:
```
wget http://localhost
```


**Python 3 HTTP Server:**
- **Python 3** can be used to start a simple HTTP server:
```
python3 -m http.server
```
- This command starts a server on port 8000 by default. Access it via [http://0.0.0.0:8000](http://0.0.0.0:8000).
- The server logs requests made to it, which can be viewed in the terminal.


### Questions:
- Find a way to start a simple HTTP server inside Pwnbox or your local VM using "npm". Submit the command that starts the web server on port 8080 (use the short argument to specify the port number).
	- http-server -p 8080
- Find a way to start a simple HTTP server inside Pwnbox or your local VM using "php". Submit the command that starts the web server on the localhost (127.0.0.1) on port 8080.
	- php -s 127.0.0.1:8080