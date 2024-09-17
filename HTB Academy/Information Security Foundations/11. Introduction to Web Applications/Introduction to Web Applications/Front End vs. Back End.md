**Front End:**
- **Definition:** Refers to the part of a web application that interacts directly with the user through their web browser (client-side).
- **Components:**
    - **HTML:** Provides the structure and content of web pages.
    - **CSS:** Controls the presentation, layout, and styling of web pages.
    - **JavaScript:** Adds interactivity and dynamic functionality to web pages.
- **Function:** Source code (HTML, CSS, JavaScript) is interpreted in real-time by the browser to render the web page as seen by the user.



**Back End:**
- **Definition:** Refers to the server-side components of a web application that handle the data processing and business logic.
- **Components:** Typically includes server-side programming languages, databases, and server configuration.



**Full Stack Web Development:**
- **Definition:** Involves both front end and back end development, covering all aspects of web application development.
- **Scope:** Full stack developers work with both client-side (front end) and server-side (back end) technologies, integrating and managing the complete development cycle of a web application.

![[frontend-components.jpg]]



**Front End:**
- **Definition:** The part of the web application that users see and interact with through their web browser (client-side).
- **Components:**
    - **HTML:** Provides the structure and content of the web page (e.g., titles, text).
    - **CSS:** Handles the design, layout, and animations of elements (e.g., styling, colors).
    - **JavaScript:** Adds functionality and interactivity (e.g., buttons, forms).
- **Optimization:**
    - Must be adaptable to various screen sizes and devices (including mobile).
    - Poor front end optimization can lead to slow or unresponsive web applications, misleading users into thinking the issue lies with the server or their internet connection.
- **Tasks Related to Front End Development:**
    - **Visual Concept Web Design:** Designing the overall look and feel of the web application.
    - **User Interface (UI) Design:** Creating the layout and interactive elements of the application.
    - **User Experience (UX) Design:** Ensuring that the application is user-friendly and provides a positive experience.
- **Practice:** Websites like coding playgrounds allow experimenting with front end code. For example, you can use an editor to see how changes in HTML, CSS, and JavaScript affect the rendering of a web page.



**Back End:**
- **Definition:** The server-side part of a web application that manages core functionalities and processes data required for the application to run.
- **Components:**
    - **Server:** Hosts and runs the web application.
    - **Web Application Logic:** Handles the processing and execution of application-specific tasks.
    - **Database:** Stores and retrieves data used by the application.
    - **API:** Facilitates communication between the server and other services or components.
- **Importance:** The back end is crucial for the web application's functionality, processing tasks, and data management. It is not directly visible to users but is essential for a functioning web application. Without a back end, a website would be a static collection of web pages.



**Back End Components:**
1. **Server:** Runs the web application and manages client requests.
2. **Web Application Logic:** Contains the code that processes requests and executes core functions.
3. **Database:** Stores data required by the application.
4. **API (Application Programming Interface):** Allows interaction between different software components or services.

![[Screenshot_20240916_134049.png]]



**Back End Isolation:**
- **Isolation Approaches:**
    - **Containers:** Use services like Docker to isolate different back end components. For example:
        - **Database Container:** Runs the database separately.
        - **Web Application Container:** Hosts the main web application.
    - **Dedicated Servers:** Each component runs on its own server, which can be more resource-intensive and complex to maintain.
- **Advantages:**
    - **Security:** Isolation reduces the risk that vulnerabilities in one component will affect others.
    - **Manageability:** Allows for better resource allocation and management based on specific needs.
- **Tasks Performed by Back End Components:**
    - Develop and maintain main logic and functionalities.
    - Manage and maintain the back end database.
    - Create and implement libraries for the application.
    - Address technical and business requirements.
    - Develop and manage APIs for communication with front end components.
    - Integrate with remote servers and cloud services.



**Securing Front/Back End:**
- **Front End:**
    - **Code Review:** When source code is accessible, perform a code review to identify vulnerabilities (Whitebox Pentesting).
- **Back End:**
    - **Default Access:** Source code is typically not accessible, leading to Blackbox Pentesting.
    - **Potential Access:** Open source applications or vulnerabilities like Local File Inclusion may provide access to the source code, allowing for a more thorough code review.
- **Common Vulnerabilities:**
    - **Injection Attacks:** SQL injections or Command Injections through improperly processed queries.
    - **Data Access:** Gaining unauthorized access to database data or executing commands on the server.


**Top 20 Common Mistakes in Web Development:**
1. Permitting Invalid Data to Enter the Database
2. Focusing on the System as a Whole
3. Establishing Personally Developed Security Methods
4. Treating Security as a Last Step
5. Developing Plain Text Password Storage
6. Creating Weak Passwords
7. Storing Unencrypted Data in the Database
8. Depending Excessively on the Client Side
9. Being Too Optimistic
10. Permitting Variables via the URL Path Name
11. Trusting Third-Party Code
12. Hard-Coding Backdoor Accounts
13. Unverified SQL Injections
14. Remote File Inclusions
15. Insecure Data Handling
16. Failing to Encrypt Data Properly
17. Not Using a Secure Cryptographic System
18. Ignoring Layer 8 (Human Factors)
19. Failing to Review User Actions
20. Web Application Firewall Misconfigurations


**OWASP Top 10 Vulnerabilities:**
1. **Broken Access Control:** Improper restrictions on user access.
2. **Cryptographic Failures:** Weak or missing encryption.
3. **Injection:** Vulnerabilities allowing injection of malicious data.
4. **Insecure Design:** Flaws in the design of the application that lead to security issues.
5. **Security Misconfiguration:** Incorrect configurations exposing the application.
6. **Vulnerable and Outdated Components:** Use of outdated or insecure components.
7. **Identification and Authentication Failures:** Weak authentication mechanisms.
8. **Software and Data Integrity Failures:** Lack of protection against data tampering.
9. **Security Logging and Monitoring Failures:** Inadequate logging and monitoring.
10. **Server-Side Request Forgery (SSRF):** Exploiting server requests to access internal systems.


**Importance for Pentesters:**
- Familiarity with these mistakes and vulnerabilities is crucial for identifying, exploiting, and explaining potential issues to clients.
- Understanding these flaws helps in performing effective penetration testing and improving application security.