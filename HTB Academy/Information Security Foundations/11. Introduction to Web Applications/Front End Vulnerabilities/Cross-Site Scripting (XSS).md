- **HTML Injection**:
    - **Definition**: HTML Injection occurs when unfiltered user input is displayed on a web page. This can involve injecting HTML code that is rendered by the browser, leading to potential security issues like displaying malicious ads or altering page content.
    - **Example**: If an input like `<a href="http://www.hackthebox.com">Click Me</a>` is used, it appears as a clickable link labeled "Click Me" that redirects to `http://www.hackthebox.com`.



- **Cross-Site Scripting (XSS)**:
    - **Definition**: XSS is a type of vulnerability that allows an attacker to inject and execute malicious JavaScript code on the client-side. This can lead to serious security risks, including the theft of sensitive information or control over the victim's session.
    - **Relation to HTML Injection**: While HTML Injection involves injecting static HTML content, XSS involves injecting and executing JavaScript code, making it more complex and potentially harmful.



- **Types of XSS**:
    - **Reflected XSS**:
        - **Description**: Occurs when user input is reflected off the web server and displayed on the page after processing. Examples include search results or error messages.
    - **Stored XSS**:
        - **Description**: Occurs when user input is stored in a back-end database and later displayed to users (e.g., comments, posts). This stored data can be served to any user who views it.
    - **DOM XSS**:
        - **Description**: Happens when user input is directly reflected in the browser’s Document Object Model (DOM) and manipulated using JavaScript (e.g., changing a page title or username).



- **Example of DOM XSS Payload**:
    - **Payload**: `#"><img src=/ onerror=alert(document.cookie)>`
    - **Effect**: When this payload is injected, it triggers an alert displaying the user's cookie value. This works by causing the browser to execute the injected JavaScript code, which accesses and displays the cookie information.
    - **Usage**: This can be used to steal session cookies and potentially gain unauthorized access to user accounts.



- **Prevention**:
    - **Input Sanitization**: Always sanitize and validate user input to prevent injection attacks.
    - **Content Security Policy (CSP)**: Implement CSP to mitigate the impact of XSS by restricting the sources from which scripts can be loaded and executed.
    - **Encoding**: Ensure that special characters are properly encoded when displaying user input on the web page.


**Note**: XSS is a complex topic with many potential attack vectors. It will be covered in more depth in subsequent modules.


## Questions
- Try to use XSS to get the cookie value in the above page
	- XSSisFun