### Notes on Web Applications and Websites

**Web Applications:**
- **Definition:** Interactive applications that run on web browsers.
- **Architecture:**
    - **Client-Server Model:**
        - **Front End:** The user interface (what users see), running on the client-side (browser).
        - **Back End:** The web application source code and databases, running on the server-side.
- **Benefits:**
    - **Real-Time Control:** Allows organizations to design and control functionality dynamically.
    - **Global Accessibility:** Available worldwide through the internet.
- **Examples:**
    - **Email Services:** Gmail.
    - **Retailers:** Amazon.
    - **Word Processors:** Google Docs.
- **Development and Hosting:**
    - Can be created by any web developer.
    - Hosted on common hosting services.
    - Millions of web applications exist, used by billions of users daily.

**Web Applications vs. Websites:**
- **Websites (Static Web 1.0):**
    - **Definition:** Static pages that do not change in real-time.
    - **Content:** Created manually and does not interact with the user.
    - **Functionality:** No real-time changes or interactive functions.
    - **Update Process:** Requires manual editing by developers to change content.


![[website_vs_webapps.jpg]]



**Web Applications vs. Traditional Websites:**
- **Web Applications (Web 2.0):**
    - **Dynamic Content:** Present content based on user interactions.
    - **Functionality:** Fully functional, offering various features to end-users.
    - **Modularity:** Designed to be modular and adaptable.
    - **Display Flexibility:** Operate on any display size and platform without specific optimization.
- **Traditional Websites (Web 1.0):**
    - **Static Content:** Fixed content that does not change in real-time.
    - **Functionality:** Lacks interactive features and requires manual updates for content changes.
    - **Update Process:** Content changes require manual editing by developers.



**Web Applications vs. Native OS Applications:**
- **Web Applications:**
    - **Platform Independence:** Can run in any browser across different operating systems.
    - **No Installation Needed:** Functionality is executed remotely, saving space on the user's device.
    - **Version Unity:** All users access the same version, and updates are made centrally, reducing maintenance and support costs.
    - **Updates:** Can be updated on the webserver without developing separate builds for each platform.
- **Native OS Applications:**
	- **Performance:** Faster operation due to deeper integration with the operating system and use of native libraries.
	- **Capabilities:** Generally more capable due to direct access to local hardware and system resources.
	- **Hybrid/Progressive Web Applications:** Combine web and native capabilities to offer improved performance and functionality.


**Web Application Distribution:**
- **Open-Source Web Applications:**
    - Examples: WordPress, OpenCart, Joomla.
    - **Customization:** Can be tailored to meet specific organizational needs.
- **Proprietary 'Closed Source' Web Applications:**
    - Examples: Wix, Shopify, DotNetNuke.
    - **Subscription Model:** Developed by organizations and sold or used through subscriptions.



**Security Risks of Web Applications:**
- **Vulnerabilities:**
    - **Exposure:** Accessible globally, leading to a large attack surface.
    - **Attack Tools:** Automated tools can exploit vulnerabilities if misused.
    - **Critical Vulnerabilities:** More complex applications may have serious design flaws.
- **Penetration Testing:**
    - **Importance:** Essential for identifying and mitigating vulnerabilities.
    - **OWASP Web Security Testing Guide:** A common method for testing web application security.
    - **Testing Focus:**
        - Front-end components (HTML, CSS, JavaScript) for vulnerabilities.
        - Core functionality and interactions between browser and server.
        - Both unauthenticated and authenticated perspectives to maximize coverage.
- **Common Vulnerabilities:**
    - **SQL Injection:** Exploits unsafe handling of user input, leading to data breaches or remote code execution.
    - **File Inclusion:** Allows reading source code or accessing unauthorized files.
    - **Unrestricted File Upload:** Uploads malicious code disguised as regular files.
    - **Insecure Direct Object Referencing (IDOR):** Allows access to other users' files or functionality.
    - **Broken Access Control:** Misconfigured user roles can lead to unauthorized access or privilege escalation.



**Real-World Examples:**
- **SQL Injection:** Extracting Active Directory usernames for further attacks.
- **File Inclusion:** Finding hidden pages or directories for exploitation.
- **Unrestricted File Upload:** Gaining control over the web server by uploading malicious code.
- **IDOR:** Editing other users' profiles by manipulating URL parameters.
- **Broken Access Control:** Registering with elevated privileges to access restricted features.