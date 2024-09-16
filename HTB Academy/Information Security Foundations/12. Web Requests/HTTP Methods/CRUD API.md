### Notes on Interacting with APIs for CRUD Operations

**Overview:**
- This section covers how a City Search web application uses APIs to perform CRUD (Create, Read, Update, Delete) operations on city data.

**API Interaction:**
- APIs interact with databases by specifying tables and rows in queries.
- Different HTTP methods perform various operations on data.

**HTTP Methods for CRUD Operations:**
- **Create (POST):** Adds new data to the database.
- **Read (GET):** Retrieves data from the database.
- **Update (PUT):** Modifies existing data in the database.
- **Delete (DELETE):** Removes data from the database.

**Examples of Using APIs:**
1. **Read Operation:**
    - Retrieve data by specifying the table and search term in the URL.
    - Example: Use `curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq` to get data for "London".
    - Search with a partial term or an empty string to get matching results or all entries.
2. **Create Operation:**
    - Add new data using a POST request with JSON data.
    - Example: Use `curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'` to add a city.
    - Confirm the addition by retrieving the new city.
3. **Update Operation:**
    - Update existing data with a PUT request.
    - Example: Use `curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'` to update "London" to "New_HTB_City".
    - Confirm the update by retrieving both the old and new entries.
4. **Delete Operation:**
    - Remove data using a DELETE request.
    - Example: Use `curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City` to delete "New_HTB_City".
    - Confirm deletion by attempting to retrieve the deleted city.

**Notes:**
- **PATCH Method:** Used for partial updates (e.g., modifying only some fields).
- **OPTIONS Method:** Can be used to check which methods are supported by the server.
- **User Authentication:** Real applications require authentication to limit access. This can be done with cookies or authorization headers (e.g., JWT).

**Exercises:**
1. Add a new city using browser devtools and fetch POST requests.
2. Update a non-existing city and observe the API behavior.
3. Delete cities added earlier and verify their removal.

## Questions
- First, try to update any city's name to be 'flag'. Then, delete any city. Once done, search for a city named 'flag' to get the flag.
	- HTB{crud_4p!_m4n!pul4t0r}