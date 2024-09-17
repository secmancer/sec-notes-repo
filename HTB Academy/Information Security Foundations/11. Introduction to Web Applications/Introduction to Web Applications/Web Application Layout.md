### Notes on Web Application Layout and Infrastructure



**Overview:**
- **Uniqueness:** No two web applications are identical; they vary based on business needs, design, and backend infrastructure.
- **Importance:** Understanding web application setups, structures, and components is crucial for effective management and security.



**Web Application Layout Categories:**
1. **Web Application Infrastructure:**
    - **Description:** Refers to the structure of required components such as databases necessary for the web application’s functionality.
    - **Importance:** Knowing the infrastructure helps identify which database server the application needs to access, especially if the application runs on a separate server.
2. **Web Application Components:**
    - **Description:** Components that interact to form the web application, divided into:
        - **UI/UX:** User Interface and User Experience components.
        - **Client:** Components that run on the client-side (browser).
        - **Server:** Components that run on the server-side (backend logic, databases).
3. **Web Application Architecture:**
    - **Description:** The overall design of the web application, including the relationships and interactions between various components.

**Web Application Infrastructure Models:**
1. **Client-Server:**
    - **Description:** A model where the server hosts the web application and distributes it to clients (users) who access it through their browsers.
    - **Common Use:** Frequently used in web applications to separate the server-side logic from the client-side interface.
2. **One Server:**
    - **Description:** A single server handles both the application and the database.
    - **Common Use:** Suitable for smaller applications or during development and testing phases.
3. **Many Servers - One Database:**
    - **Description:** Multiple servers manage the web application while accessing a single database.
    - **Common Use:** Provides scalability and load balancing for handling high traffic.
4. **Many Servers - Many Databases:**
    - **Description:** Multiple servers and databases are used to manage the web application.
    - **Common Use:** Often used for large-scale applications requiring high availability, redundancy, and distributed data management.

![[client-server-model.jpg]]

**Components of Web Applications:**
1. **Front End:**
    - **Description:** Components that run on the client-side (browser).
    - **Execution:** Interpreted and executed in the user's browser.
    - **Function:** Includes UI elements like buttons, forms, and displays that interact with the user.
2. **Back End:**
    - **Description:** Components that run on the server-side.
    - **Execution:** Compiled or interpreted and executed by the hosting server.
    - **Function:** Handles data processing, server-side logic, database interactions, and more.



**Client-Server Interaction:**
- **User Request:**
    - **Process:** When a user visits a web application URL (e.g., [https://www.acme.local](https://www.acme.local)), the server uses the main web application interface (UI).
    - **Action:** When a user interacts with the UI (e.g., clicking a button or requesting a function), the browser sends an HTTP request to the server.
- **Server Response:**
    - **Process:** The server interprets the request and performs the required tasks (e.g., logging in, adding items to a cart).
    - **Action:** After processing, the server sends the result back to the client’s browser.
    - **Display:** The result is displayed in a human-readable format on the client-side.



**Example:**
- **Current Interaction:** The website you are interacting with is a web application developed and hosted by Hack The Box. You access and interact with it through your web browser.




**Web Application Design Implementations:**
1. **One Server:**
    - **Description:** All components of the web application, including the database, are hosted on a single server.
    - **Pros:** Simple to set up and implement.
    - **Cons:** Risky due to single point of failure; if the server fails, the entire application and database become inaccessible.


![[one-server-arch.jpg]]

**One Server Architecture:**
- **Risk:** If any web application hosted on the server is compromised, all web applications' data on that server are at risk.
- **Vulnerability:** This design represents an "all eggs in one basket" approach; a vulnerability in one application compromises the entire server.
- **Downtime:** If the server fails or goes down, all hosted web applications become inaccessible until the issue is resolved.


**Many Servers - One Database Architecture:**
- **Description:** In this model, the web applications are hosted on multiple servers, but the database is maintained on a separate, dedicated database server.
- **Function:** Web applications interact with the database server to store and retrieve data.
- **Advantages:**
    - **Separation of Concerns:** Database and application logic are separated, which can enhance security and performance.
    - **Scalability:** Multiple web servers can access the same database server, allowing for better load distribution and scalability.
- **Implementation Variants:** This model can be seen as combining the “many-servers to one-database” and “one-server to one-database” setups, as long as the database is isolated on its own server.

![[many-server-one-db-arch.jpg]]

**Many Servers - One Database:**
- **Description:** Multiple web applications access a single, dedicated database server.
- **Data Sharing:** This model allows several web applications to access the same database, ensuring consistent data access without the need for data synchronization between applications.
- **Types of Applications:** Web applications can be:
    - **Replications:** Multiple instances of a primary application (e.g., primary/backup).
    - **Separate Applications:** Independent applications sharing common data.
- **Security Advantages:**
    - **Segmentation:** Components (web servers and database) are separated. Compromise of one web server doesn’t directly impact other web servers.
    - **Database Compromise:** If the database is compromised (e.g., via SQL injection), the web application itself isn’t directly affected.
    - **Access Control:** Despite segmentation, it’s crucial to implement access controls to ensure web applications only access necessary data.



**Many Servers - Many Databases:**
- **Description:** Expands on the "Many Servers - One Database" model by separating each web application's data into its own database.
- **Data Access:** Each web application can only access its own private data and any shared data common across applications.
- **Database Hosting Options:**
    - **Separate Databases:** Each web application's data is hosted in a distinct database within a single database server.
    - **Separate Database Servers:** Each web application’s database can be hosted on its own dedicated database server.


![[many-server-many-db-arch.jpg]]


**Many Servers - Many Databases:**
- **Description:** Builds upon the "Many Servers - One Database" model by hosting each web application’s data in its own separate database.
- **Data Access:** Each web application accesses only its private data and any shared data necessary for functionality.
- **Database Hosting Options:**
    - **Separate Databases:** Each application’s data is stored in a distinct database within a single database server.
    - **Separate Database Servers:** Each application's database can be on its own dedicated server.
- **Redundancy and Redundancy Measures:**
    - **Redundancy:** Used for backup purposes to minimize downtime if a web server or database goes offline.
    - **Implementation:** May require tools like load balancers for proper functionality.
    - **Security Benefits:** Offers improved security due to proper access control and asset segmentation.



**Other Web Application Models:**
- **Serverless Web Applications:** Operate without traditional server management, using cloud-based services for scalability and maintenance.
- **Microservices Architecture:** Utilizes small, independent services that communicate over a network, offering modular and scalable solutions.



**Web Application Components:**
- **Client:** The user interface accessed through a web browser.
- **Server:**
    - **Webserver:** Hosts the web application and serves requests.
    - **Web Application Logic:** Handles application processes and business logic.
    - **Database:** Stores and manages data.
- **Services (Microservices):**
    - **3rd Party Integrations:** Interfaces with external services and APIs.
    - **Web Application Integrations:** Connects with other web applications or services.
- **Functions (Serverless):** Executes code without managing servers, triggered by events.



**Three-Tier Architecture:**
- **Presentation Layer:**
    - **Description:** UI components that interact with the user and system. Accessible via the web browser and presented in HTML, JavaScript, and CSS.
- **Application Layer:**
    - **Description:** Processes client requests, handles authorization, and manages data transactions.
- **Data Layer:**
    - **Description:** Works with the application layer to access and manage data storage.


![[image5-12.png]]

**Microservices:**
- **Definition:** Independent components of a web application, each designed for a specific task.
- **Example Components for an Online Store:**
    - Registration
    - Search
    - Payments
    - Ratings
    - Reviews
- **Communication:**
    - **Stateless:** Requests and responses are independent; data storage is separate from microservices.
    - **Service-Oriented Architecture (SOA):** Built as a collection of automated functions focused on business goals.
- **Benefits:**
    - **Agility:** Facilitates rapid development and innovation.
    - **Flexible Scaling:** Easy to scale individual components.
    - **Easy Deployment:** Streamlined deployment processes.
    - **Reusable Code:** Components can be reused across different applications.
    - **Resilience:** Fault isolation and easier recovery.
- **Language Flexibility:** Microservices can be written in different programming languages and still interact.
- **Additional Resource:** AWS whitepaper on microservice implementation.



**Serverless:**
- **Definition:** Cloud-based architecture where applications run in stateless computing containers managed by cloud providers.
- **Providers:** AWS, GCP, Azure, among others.
- **Advantages:**
    - **No Server Management:** Cloud provider handles server provisioning, scaling, and maintenance.
    - **Flexibility:** Developers can build and deploy applications without managing infrastructure.
    - **Scalability:** Applications can scale automatically based on demand.
- **Containers:** Often run in containers like Docker.
- **Additional Resource:** Further reading on serverless computing and its use cases.



**Architecture Security:**
- **Importance:** Understanding web application architecture is crucial for effective penetration testing.
- **Design Vulnerabilities:**
    - **Access Control:** Inadequate measures (e.g., lacking Role-Based Access Control (RBAC)) can expose sensitive features or user information.
    - **Database Location:** Vulnerabilities may obscure the location or existence of databases, complicating exploitation and data access.
- **Security Measures:**
    - **Phase Consideration:** Security should be integrated throughout the web application development lifecycle.
    - **Penetration Testing:** Continuous testing is necessary to identify and address architectural vulnerabilities.