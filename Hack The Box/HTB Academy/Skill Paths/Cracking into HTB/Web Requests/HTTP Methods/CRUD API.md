### APIs and CRUD Operations
- APIs (Application Programming Interfaces) allow communication between a client and a server. 
- In the context of web applications, APIs are commonly used to interact with databases to perform operations on entities such as city names in a city table. 
- The key operations are:
	1. **Create (POST)**: Adds new data to the database.
	2. **Read (GET)**: Retrieves data from the database.
	3. **Update (PUT)**: Modifies existing data in the database.
	4. **Delete (DELETE)**: Removes data from the database.
- Each of these operations is performed using the corresponding HTTP methods.
- For example, to add a new city, we use a POST request with the required data in JSON format.



### CRUD Operations with cURL
- We used the `curl` command to interact with the API. 
- Here's a brief overview of how we can perform each operation using `curl`:
1. **Read**:
    - Use the `GET` method to retrieve data.
    - Example:
        ```bash
        curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
        ```
2. **Create**:
    - Use the `POST` method to add a new entry.
    - Example:
        ```bash
        curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
        ```
3. **Update**:
    - Use the `PUT` method to modify an existing entry.
    - Example:
        ```bash
        curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
        ```
4. **Delete**:
    - Use the `DELETE` method to remove an entry.
    - Example:
        ```bash
        curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
        ```



### Using JSON and Authentication
- **JSON**: We often interact with APIs that require data to be sent in JSON format. We can set the `Content-Type` to `application/json` to specify the format.
- **Authentication**: Many APIs require authentication (e.g., via cookies or JWT tokens) to access or modify data.



### Practical Exercises
- **Create**: Try adding new entries to the database using POST requests.
- **Update**: Use the PUT method to update data. Experiment with updating a non-existing entry.
- **Delete**: Use the DELETE method to remove entries. Confirm by checking the database after deletion.
- By understanding and practicing these operations, you can efficiently interact with web application APIs for tasks like bug bounty hunting or security assessments.



### Questions
- First, try to update any city's name to be 'flag'. Then, delete any city. Once done, search for a city named 'flag' to get the flag.
	- HTB{crud_4p!_m4n!pul4t0r}