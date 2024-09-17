**Back-End Server Overview**
- **Definition**:
    - The back-end server is the hardware and operating system that hosts the applications necessary to run a web application. It performs all the processes and tasks required for the web application's functionality.
- **Components of the Back-End Server**:
    1. **Web Server**:
        - **Role**: Manages and serves HTTP requests from clients (e.g., browsers) and delivers web content.
        - **Examples**: Apache, Nginx, Microsoft IIS.
    2. **Database**:
        - **Role**: Stores, retrieves, and manages data used by the web application.
        - **Examples**: MySQL, PostgreSQL, MongoDB, Oracle Database.
    3. **Development Framework**:
        - **Role**: Provides a structured environment for building and maintaining web applications. It includes libraries, tools, and best practices for application development.
        - **Examples**: Django, Ruby on Rails, Express.js, Spring Boot.
- **Data Access Layer**:
    - The back-end server fits within the data access layer, which is responsible for managing the interaction between the application and the data sources. This layer handles data retrieval, storage, and management.

![[backend-server.jpg]]

- **Additional Software Components**:
    1. **Hypervisors**:
        - **Role**: Manage virtual machines (VMs) on a physical server, allowing multiple operating systems to run concurrently on a single hardware platform.
        - **Examples**: VMware ESXi, Microsoft Hyper-V, Xen.
    2. **Containers**:
        - **Role**: Package applications and their dependencies into a single, portable container that can be deployed across various environments.
        - **Examples**: Docker, Kubernetes.
    3. **Web Application Firewalls (WAFs)**:
        - **Role**: Protect web applications by filtering and monitoring HTTP requests to prevent attacks such as SQL injection, XSS, and other vulnerabilities.
        - **Examples**: ModSecurity, AWS WAF, Cloudflare WAF.
- **Common Back-End Stacks**:
    - **LAMP**:
        - **Components**: Linux, Apache, MySQL, PHP.
    - **WAMP**:
        - **Components**: Windows, Apache, MySQL, PHP.
    - **WINS**:
        - **Components**: Windows, IIS, .NET, SQL Server.
    - **MAMP**:
        - **Components**: macOS, Apache, MySQL, PHP.
    - **XAMPP**:
        - **Components**: Cross-Platform, Apache, MySQL, PHP/PERL.
    - **Resource**: For a comprehensive list of Web Solution Stacks, refer to relevant articles or documentation.
        
- **Hardware**:
    - **Role**: Provides the physical resources necessary to support the web application's operations. The power and performance capabilities of the hardware impact the stability and responsiveness of the application.
    - **Examples**: Servers, storage devices, networking equipment.
    - **Architecture**:
        - **Scalability**: Large web applications may use multiple back-end servers distributed across data centers or cloud hosting services to handle the load and ensure reliability.
        - **Virtualization**: Web applications may run on virtual hosts provided by cloud services, which offer flexibility and scalability beyond a single physical server.


## Questions
- What operating system is 'WAMP' used with?
	- Windows