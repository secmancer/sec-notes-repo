### Introduction
- **Web Applications**: Interactive applications that run on web browsers, offering functionalities such as online email, retail, and word processing.
- **Client-Server Architecture**: Web applications typically use a client-server model, with front-end components running on the client side (browser) and back-end components running on the server side (server/databases).
- **Global Accessibility**: Web applications can be hosted by organizations, offering powerful tools with near-complete control over design and functionality while being accessible worldwide.
- **Wide Availability**: Web applications are not limited to large providers like Google or Microsoft; they can be developed by anyone and hosted on common services, making them widely available on the internet.
- **Ubiquity**: Millions of web applications are used by billions of people daily.



### Web Applications vs. Websites
- **Web 1.0 (Traditional Websites)**: Static websites with fixed content that do not change in real-time based on user interaction. Content updates require manual editing by developers.
- **Web 2.0 (Web Applications)**: Dynamic websites that present content based on user interaction and perform various functionalities. Web applications are fully functional and respond to user input in real-time.
- **Key Differences**:
    - **Modularity**: Web applications are often modular, allowing for more flexible updates and maintenance.
    - **Responsive**: Web applications are designed to run on any display size, adjusting to different devices and screen resolutions.
    - **Cross-Platform Compatibility**: Web applications run on various platforms without the need for optimization specific to each.
![web sites vs web apps](https://academy.hackthebox.com/storage/modules/75/website_vs_webapps.jpg)



### Web Applications vs. Native Operating System Applications
- **Web Applications**: Platform-independent and run in a browser on any operating system, without needing installation on the user's system. The functionality is executed remotely on a server, saving space on the user's hard drive.
    - **Version Unity**: All users access the same version of the web application, allowing for continuous updates at the server level without needing to push updates to each individual user.
    - **Reduced Maintenance**: Web applications can be updated centrally, which reduces maintenance and support costs, eliminating the need to notify or manage updates for each user individually.
- **Native OS Applications**: Built to operate on specific operating systems and utilize native OS libraries and hardware, making them faster and more capable than web applications. They are not limited to the capabilities of a browser.
    - **Speed & Capability**: Native applications load and interact more quickly due to their deeper integration with the operating system.
- **Hybrid and Progressive Web Applications (PWA)**: Emerging technologies that combine the advantages of both web and native applications, using modern frameworks to leverage native OS capabilities, improving performance and capabilities compared to traditional web applications.



### Web Application Distribution
- There are many open-source web applications used by organizations worldwide that can be customized to meet each organization's needs. 
- Some common open source web applications include:
	- [WordPress](https://wordpress.com/)
	- [OpenCart](https://www.opencart.com/)
	- [Joomla](https://www.joomla.org/)
- There are also proprietary 'closed source' web applications, which are usually developed by a certain organization and then sold to another organization or used by organizations through a subscription plan model. 
- Some common closed source web applications include:
	- [Wix](https://www.wix.com/)
	- [Shopify](https://www.shopify.com/)
	- [DotNetNuke](https://www.dnnsoftware.com/)



### Security Risks of Web Applications
- **Prevalence of Web Application Attacks**: Web applications are accessible globally, offering a large attack surface, making them attractive targets for attackers. The complexity of modern web applications increases the likelihood of critical vulnerabilities being present in their design.
- **Impact of Successful Attacks**: Attacks on web applications can lead to significant data breaches, business interruptions, and compromise of sensitive information, including data stored in databases connected to the application.
- **Importance of Security Testing**: Regular testing for vulnerabilities and prompt patching is essential to securing web applications. Testing should verify that patches fix flaws without introducing new ones.
- **Penetration Testing and Secure Coding**: Web application penetration testing is crucial for organizations to secure their web applications, both internal and external. Secure coding practices should be implemented throughout the development life cycle.
- **OWASP Web Security Testing Guide**: The OWASP Web Security Testing Guide is a widely used framework for testing web applications, beginning with a review of the front end components (HTML, CSS, JavaScript) for vulnerabilities such as Sensitive Data Exposure and Cross-Site Scripting (XSS).
- **Testing Methodology**: Web applications should be tested from both an unauthenticated and authenticated perspective to ensure comprehensive coverage. This involves reviewing the application's front end and core functionality, as well as evaluating the interaction between the browser and web server to identify exploitable flaws.



### Attacking Web Applications
- **Prevalence of Web Applications**: Most companies, regardless of size, have one or more web applications, ranging from simple websites to complex applications with user roles, such as super admins and regular users. These applications often present a significant attack surface due to their dynamic nature and constant updates.
- **Potential Vulnerabilities**: Code changes in web applications can introduce critical vulnerabilities, including SQL injection and file upload flaws, leading to unauthorized access, remote code execution, or data leaks. These vulnerabilities may allow attackers to gain control of the server or access sensitive data.
- **SQL Injection and Active Directory**: SQL injection remains a common vulnerability, particularly in web applications using Active Directory for authentication. While attackers may not directly extract passwords from Active Directory, they can retrieve user email addresses, which are often used as usernames. This can enable password spraying attacks against services like VPNs and Microsoft O365, potentially granting access to sensitive data or even a foothold in the corporate network.
- **Chaining Vulnerabilities**: Web application vulnerabilities can often be chained together to exploit other parts of the organization's infrastructure. For example, extracting data from one web application may facilitate attacks on other services within the network, highlighting the interconnected risks.
- **Importance of Web Application Expertise**: Understanding web applications is essential for a well-rounded infosec professional. Penetration testers with a solid foundation in web application security can identify vulnerabilities that others might miss, setting them apart and enhancing their ability to detect security flaws across various systems and networks.
- **Web Application Attacks**: Familiarizing yourself with common web application attacks and their implications is crucial. Even if some terms seem unfamiliar initially, you will gain a deeper understanding through hands-on practice and a step-by-step learning approach.
- **Iterative Learning**: Web application attacks will be a recurring theme throughout your journey, both in the HTB Academy and real-world assessments. By progressively studying these attacks, you will refine your skills and knowledge over time.
- **Understanding Web Application Structure**: It's essential to deeply understand the inner workings of web applications and their various tech stacks. A solid foundation will allow you to identify vulnerabilities more effectively.
- **Becoming an Informed Attacker**: By learning the structure and function of web applications, you'll become better-equipped to spot flaws others may overlook. This expertise will set you apart from your peers and give you an edge in penetration testing and vulnerability assessment.

| Flaw | Real-world Scenario |
| --- | --- |
| [SQL injection](https://owasp.org/www-community/attacks/SQL_Injection) | Obtaining Active Directory usernames and performing a password spraying attack against a VPN or email portal. |
| [File Inclusion](https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/07-Input_Validation_Testing/11.1-Testing_for_Local_File_Inclusion) | Reading source code to find a hidden page or directory which exposes additional functionality that can be used to gain remote code execution. |
| [Unrestricted File Upload](https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload) | A web application that allows a user to upload a profile picture that allows any file type to be uploaded (not just images). This can be leveraged to gain full control of the web application server by uploading malicious code. |
| [Insecure Direct Object Referencing (IDOR)](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html) | When combined with a flaw such as broken access control, this can often be used to access another user's files or functionality. An example would be editing your user profile browsing to a page such as /user/701/edit-profile. If we can change the `701` to `702`, we may edit another user's profile! |
| [Broken Access Control](https://owasp.org/www-project-top-ten/2017/A5_2017-Broken_Access_Control) | Another example is an application that allows a user to register a new account. If the account registration functionality is designed poorly, a user may perform privilege escalation when registering. Consider the `POST` request when registering a new user, which submits the data `username=bjones&password=Welcome1&email=bjones@inlanefreight.local&roleid=3`. What if we can manipulate the `roleid` parameter and change it to `0` or `1`. We have seen real-world applications where this was the case, and it was possible to quickly register an admin user and access many unintended features of the web application. |
