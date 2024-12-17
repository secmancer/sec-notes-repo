### Introduction
- Most modern applications interact with the internet through web requests using the HTTP protocol.
- HTTP is an application-level protocol designed to access web resources.
- The term "hypertext" refers to text that includes links to other resources, easily interpretable by readers.
- HTTP communication involves a client requesting resources from a server, which processes the request and returns the resource.
- The default port for HTTP is `80`, but this can be changed based on web server configurations.
- URLs like `http://www.hackthebox.com` use Fully Qualified Domain Names (FQDNs) to locate websites.

### URL
- Resources over HTTP are accessed via a `URL`,
- This offers many more specifications than simply specifying a website we want to visit.
![[Screenshot_20241107_154319.png]]
- Not all components are required to access a resource. 
- The main mandatory fields are the scheme and the host, without which the request would have no resource to request.


### HTTP Flow
![[HTTP_Flow_png.png]]
- The diagram shows the anatomy of an HTTP request at a high level.
- When a user enters a URL (e.g., `inlanefreight.com`) into the browser, it sends a request to a DNS server to resolve the domain and obtain its IP address.
- The DNS server looks up the IP address for the domain and returns it.
- Servers require IP addresses to communicate, so all domain names must be resolved this way.

> **Note:** Our browsers usually first look up records in the local '`/etc/hosts`' file, and if the requested domain does not exist within it, then they would contact other DNS servers. We can use the '`/etc/hosts`' to manually add records to for DNS resolution, by adding the IP followed by the domain name.

- Once the browser gets the IP address for the requested domain, it sends a GET request to the default HTTP port (e.g., `80`), asking for the root (`/`) path.
- The web server receives the request and processes it. By default, servers return an index file (e.g., `index.html`) when a request for `/` is made.
- The contents of `index.html` are read and returned by the web server as an HTTP response.
- The response also includes a status code (e.g., `200 OK`), indicating that the request was successfully processed.
- The web browser then renders the `index.html` contents and presents them to the user.

> **Note:** This module is mainly focused on HTTP web requests. For more on HTML and web applications, you may refer to the [Introduction to Web Applications](https://academy.hackthebox.com/module/details/75) module.


### cURL
- In this module, we will be sending web requests using two key tools: a Web Browser (like Chrome or Firefox) and the `cURL` command-line tool.
- **cURL** ([curl.haxx.se](https://curl.haxx.se/)) is a powerful command-line tool and library that supports multiple protocols, making it essential for automation and scripting in web penetration tests.
- We can send basic HTTP requests using cURL by providing a URL as an argument.
```shell-session
secmancer@htb[/htb]$ curl inlanefreight.com

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```
- We see that cURL does not render the HTML/JavaScript/CSS code like a web browser, but instead, it outputs it in its raw format. However, as penetration testers, we are often more focused on the request and response context, which makes cURL faster and more convenient.
- cURL can also be used to download entire pages or files and save them to a local file using the `-O` flag to save the file with its original name or `-o` followed by a custom file name.
```shell-session
secmancer@htb[/htb]$ curl -O inlanefreight.com/index.html
secmancer@htb[/htb]$ ls
index.html
```
- As we can see, the output was not printed this time but rather saved into `index.html`. 
- We noticed that cURL still printed some status while processing the request. 
- We can silent the status with the `-s` flag.
```shell-session
secmancer@htb[/htb]$ curl -s -O inlanefreight.com/index.html
```
- This time, cURL did not print anything, as the output was saved into the `index.html` file. 
- Finally, we may use the `-h` flag to see what other options we may use with cURL.
```shell-session
secmancer@htb[/htb]$ curl -h
Usage: curl [options...] <url>
 -d, --data <data>   HTTP POST data
 -h, --help <category> Get help for commands
 -i, --include       Include protocol response headers in the output
 -o, --output <file> Write to file instead of stdout
 -O, --remote-name   Write output to a file named as the remote file
 -s, --silent        Silent mode
 -u, --user <user:password> Server user and password
 -A, --user-agent <name> Send User-Agent <name> to server
 -v, --verbose       Make the operation more talkative

This is not the full help, this menu is stripped into categories.
Use "--help category" to get an overview of all categories.
Use the user manual `man curl` or the "--help all" flag for all options.
```
- As mentioned above, we can use `--help all` to display a comprehensive help menu or `--help category` (e.g., `-h http`) to get detailed information on specific flags.
- If we need more in-depth documentation, we can use `man curl` to access the full cURL manual page.
- In the upcoming sections, we will explore many of the flags discussed here and understand how to apply them effectively in different scenarios.

### Questions
- To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above.
	- HTB{64$!c_cURL_u$3r}