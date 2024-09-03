### Web Servers on Linux

**Apache Web Server**

- **Overview**: Apache is a widely used web server software. It supports modules for encryption (mod_ssl), proxy functionality (mod_proxy), HTTP header manipulation (mod_headers), and URL rewriting (mod_rewrite).
- **Dynamic Pages**: Apache allows dynamic page creation using scripting languages such as PHP, Perl, Ruby, Python, JavaScript, Lua, and .NET.
- **Installation**: sudo apt install apache2 -y
- **Verify Installation**: After starting Apache, navigate to `http://localhost` to see the default page, confirming that the server is running correctly.

**cURL**

- **Overview**: cURL is a tool for transferring files over various protocols (HTTP, HTTPS, FTP, SFTP, etc.). It helps test and control websites remotely.
- **Usage**: curl http://localhost


**Wget**

- **Overview**: wget is a tool for downloading files from FTP or HTTP servers. It is useful as a download manager.
- **Usage**: wget http://localhost


**Python 3 Web Server**

- **Overview**: Python 3 provides a simple way to start a web server from the terminal. This is often used for quick file transfers or testing.
- **Installation**: sudo apt install python3 -y
- **Start Server**: python3 -m http.server
- **Usage**: Access the server at `http://0.0.0.0:8000/`. Python 3 web server logs requests, which can be viewed in the terminal.