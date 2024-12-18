### Introduction
- **Web development frameworks** simplify the creation of modern web applications by providing pre-built functionality for common tasks like user registration.
- Popular frameworks help developers quickly implement core features and integrate them with frontend components, saving time and effort.
- Common frameworks include:
    - **Laravel** (PHP): Popular with startups and smaller companies for its power and ease of use.
    - **Express** (Node.js): Used by large companies like PayPal, Yahoo, and Uber.
    - **Django** (Python): Utilized by Google, YouTube, Instagram, and others.
    - **Rails** (Ruby): Previously used by Twitter and now used by GitHub, Hulu, and Airbnb.
- Popular websites typically use a mix of frameworks and web servers, rather than relying on just one.


### APIs
- **Web APIs** and **HTTP request parameters** are crucial for connecting the front end and back end of a web application, enabling data exchange and function execution.
- Front end components use APIs to send requests to the back end for specific tasks, passing necessary input.
- The back end processes these requests, performs the required functions, and sends responses back to the front end, which then renders the final output for the user.



### Query Parameters
- **GET** and **POST** request parameters are commonly used to send specific arguments to a web page, allowing the front end to pass values for processing by the back end.
- For example, a `/search.php` page could take an `item` parameter for a search query, such as `/search.php?item=apples` for a GET request or through POST data for a POST request.
- Query parameters enable pages to handle various types of input, and Web APIs may offer a quicker and more efficient solution in certain cases. The **Web Requests module** provides further insights into **HTTP** requests.
```http
POST /search.php HTTP/1.1
...SNIP...

item=apples
```



### Web APIs
- An **API** (Application Programming Interface) specifies how applications can interact, and for web applications, it enables remote access to back end functionality over the **HTTP** protocol, typically handled through web servers.
- For example, a weather API might return current weather data for a city in **JSON** format when provided with the city name or ID, while Twitter's API can fetch the latest tweets or post new ones (if authenticated) in **XML** or **JSON** formats.
- Developers implement APIs in web applications using standards like **SOAP** or **REST** to enable communication between the front end and back end.
![API examples](https://academy.hackthebox.com/storage/modules/75/api_examples.jpg)



### SOAP
- **SOAP** (Simple Object Access Protocol) shares data using **XML**, where both the request and response are formatted in XML, and front end components are designed to parse this XML output. SOAP is ideal for transferring structured data or binary data, including serialized objects, making it suitable for sharing complex data between front and back end components.
- SOAP is also valuable for sharing **stateful** objects, which allows the transfer and modification of the current state of a web page, often used in modern web and mobile applications.
- However, SOAP can be challenging for beginners and may involve lengthy and complicated requests, even for simple queries. In contrast, the **REST** API standard is often preferred for more straightforward interactions.
```xml
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



### REST
- **REST** (Representational State Transfer) shares data through the **URL path** (e.g., `search/users/1`), typically returning the output in **JSON** format (e.g., `userid 1`).
- Unlike **query parameters**, REST APIs focus on pages expecting a single input passed directly through the URL path, making it suitable for actions like **search**, **sort**, or **filter**. This modularity enhances the scalability of web applications by breaking down functionality into smaller, more manageable API requests.
- REST API responses are often in **JSON** format, though other formats like **XML**, **x-www-form-urlencoded**, or raw data can be used. The front end handles and renders these responses appropriately.
- **REST** uses different **HTTP methods** for various actions:
    - `GET`: Retrieve data
    - `POST`: Create data (non-idempotent)
    - `PUT`: Create or replace existing data (idempotent)
    - `DELETE`: Remove data
```json
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



### Questions
- Use GET request '/index.php?id=0' to search for the name of the user with id number 1?
	- superadmin