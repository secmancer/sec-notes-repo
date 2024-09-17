**Front End Components**:
- **Client-Side Interaction**: Front end components (HTML, CSS, JavaScript) are executed in the browser. They are less likely to cause permanent damage to the back end but can expose end-users to vulnerabilities.
- **Potential Risks**: Vulnerabilities in the front end can lead to unauthorized access, sensitive data exposure, and service disruptions, especially if exploited by attacking admin users.



**Sensitive Data Exposure**:
- **Definition**: Refers to sensitive data being exposed in clear-text in the front end, such as in HTML source code or JavaScript.
- **Viewing Source Code**: Users can view the page source by right-clicking and selecting "View Page Source," or by pressing `Ctrl + U`. This can reveal sensitive information like credentials or hidden links.
- **Example**: A login form's source code might contain developer comments with test credentials:
```
<!-- TODO: remove test credentials test:test -->
```


**Potential Findings**:
- **Sensitive Data**: Login credentials, hashes, or other sensitive data in comments or external JavaScript files.
- **Exposed Information**: Links, directories, or user information that can be used to further access or attack the web application or its infrastructure.



**Review and Prevention**:
- **Source Code Review**: Always review the front end source code for unnecessary comments, exposed credentials, or hidden links. Automated tools can assist in scanning for vulnerabilities and sensitive information.
- **Data Classification and Controls**: Ensure that only necessary code is visible to users. Apply controls on what data is exposed client-side.
- **Code Packing/Obfuscation**: Use techniques like JavaScript obfuscation to reduce the risk of exposing sensitive data. This makes it harder for automated tools to locate sensitive information.


## Questions
- Check the above login form for exposed passwords. Submit the password as the answer.
	- HiddenInPlainSight