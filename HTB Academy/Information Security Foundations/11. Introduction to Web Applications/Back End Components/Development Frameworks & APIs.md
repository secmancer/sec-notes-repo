### Web Development Framew
In web development, frameworks streamline the creation of web applications by providing a structured foundation for common tasks and functionality. They help manage complexity and enhance productivity. Here are some popular web development frameworks:
- **Laravel (PHP)**
    - **Usage**: Popular with startups and smaller companies.
    - **Strengths**: Powerful, yet user-friendly, facilitating rapid development.
- **Express (Node.js)**
    - **Usage**: Employed by companies like PayPal, Yahoo, Uber, IBM, and MySpace.
    - **Strengths**: Minimalist and flexible, suitable for building robust web applications and APIs.
- **Django (Python)**
    - **Usage**: Utilized by major sites like Google, YouTube, Instagram, Mozilla, and Pinterest.
    - **Strengths**: High-level framework that encourages rapid development and clean, pragmatic design.
- **Rails (Ruby)**
    - **Usage**: Used by GitHub, Hulu, Twitch, Airbnb, and previously by Twitter.
    - **Strengths**: Convention over configuration, emphasizing simplicity and productivity.


**Note**: Popular websites often use a mix of frameworks and web servers to meet their needs, rather than relying on a single solution.


### APIs (Application Programming Interfaces)
APIs are crucial for enabling communication between the front end and back end of web applications. They facilitate the exchange of data and functionality across different components and applications.
- **Function**: Allows front end components to request tasks from the back end and receive responses.
- **Usage**: APIs handle requests and responses, making it possible for the web application to interact with other services and systems.


### Query Parameters
Query parameters are used to pass specific arguments to web pages, typically in GET and POST requests.
- **GET Request**: Parameters are included in the URL.
    - **Example**: `/search.php?item=apples`
- **POST Request**: Parameters are included in the request body.
    - **Example**:
```
POST /search.php HTTP/1.1
...SNIP...

item=apples
```
Query parameters enable pages to process various types of input and customize responses accordingly.


### Web APIs
- **Definition**: An interface that allows applications to interact with each other over the web.
- **Access**: Typically accessed via the HTTP protocol and managed by web servers.
- **Function**: Provides a means for front end and back end components to communicate, enabling dynamic data exchange and functionality.


![[api_examples.jpg]]

**Weather Web Application Example**
- **Function**: Retrieves current weather for a city.
- **Request**: API URL with city name or city ID.
- **Response**: JSON object containing weather details.



**Twitter API Example**
- **Function**: Retrieves latest Tweets from a certain account.
- **Request**: API URL to get Tweets.
- **Response**: XML or JSON formats.
- **Functionality**: Allows sending Tweets if authenticated.


**SOAP (Simple Object Access Protocol)**
- **Data Format**: XML.
- **Request/Response**: Requests and responses are in XML format.
- **Example SOAP Message**:
```
<?xml version="1.0"?>

<soap:Envelope
xmlns:soap="http://www.example.com/soap/soap/"
soap:encodingStyle="http://www.w3.org/soap/soap-encoding">

<soap:Header>
</soap:Header>

<soap:Body>
  <soap:Fault>
  </soap:Fault>
</soap:Body>

</soap:Envelope>
```

**Advantages**:
- Useful for transferring structured data or binary data.
- Good for sharing complex data and stateful objects.
**Disadvantages**:
- Can be complicated and verbose.
- May require longer requests for simpler queries.



**REST (Representational State Transfer)**
- **Data Format**: Typically JSON, but can also include XML, x-www-form-urlencoded, or raw data.
- **Request/Response**: Data is shared through URL paths and responses are often in JSON.
- **Example JSON Response** for `GET /category/posts/`:
```
{
  "100001": {
    "date": "01-01-2021",
    "content": "Welcome to this web application."
  },
  "100002": {
    "date": "02-01-2021",
    "content": "This is the first post on this web app."
  },
  "100003": {
    "date": "02-01-2021",
    "content": "Reminder: Tomorrow is the ..."
  }
}
```
**Advantages**:
- Simpler and more flexible compared to SOAP.
- Focuses on resources and actions through URLs.
- Modular and scalable by breaking down functionality into smaller APIs.
**HTTP Methods**:
    - **GET**: Retrieve data.
    - **POST**: Create data (non-idempotent).
    - **PUT**: Create or replace existing data (idempotent).
    - **DELETE**: Remove data.


## Questions
- Use GET request '/index.php?id=0' to search for the name of the user with id number 1?
	- superadmin