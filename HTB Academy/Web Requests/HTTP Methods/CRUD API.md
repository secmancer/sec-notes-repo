ChatGPT
Working with APIs: CRUD Operations

APIs (Application Programming Interfaces) allow interaction with web applications and databases using HTTP methods. Here’s how to perform CRUD operations on an API endpoint:
1. Read Data

To retrieve data from an API:

    Use a GET request to fetch information.
    For example, accessing http://<SERVER_IP>:<PORT>/api.php/city/london will provide information about London.
    To format the JSON output, you can pipe it through jq, using curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq.

You can also:

    Search for cities with a term: curl -s http://<SERVER_IP>:<PORT>/api.php/city/le | jq.
    Retrieve all entries: curl -s http://<SERVER_IP>:<PORT>/api.php/city/ | jq.

2. Create Data

To add a new entry:

    Use a POST request with JSON data.
    For instance, sending data to http://<SERVER_IP>:<PORT>/api.php/city/ with {"city_name":"HTB_City", "country_name":"HTB"} and setting the Content-Type to application/json will add a new city.

Verify by retrieving the new city:

    Check it with curl -s http://<SERVER_IP>:<PORT>/api.php/city/HTB_City | jq.

3. Update Data

To modify an existing entry:

    Use a PUT request specifying the entity to be updated in the URL.
    For example, updating London to a new city New_HTB_City can be done with curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'.

Verify the update:

    Check the old city name to confirm it no longer exists: curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq.
    Check the new city: curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq.

4. Delete Data

To remove an entry:

    Use a DELETE request.
    For instance, delete New_HTB_City with curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City.

Verify deletion:

    Check that the entry no longer exists: curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq.

Exercises

    Create and Verify: Add a new city using browser DevTools and confirm it with a GET request.
    Update and Verify: Change the name of an existing city with a PUT request and check both old and new names.
    Delete and Confirm: Remove a city with DELETE and verify its absence with a GET request.

Notes

    HTTP Methods:
        POST: Add data.
        GET: Retrieve data.
        PUT: Update data.
        DELETE: Remove data.
        PATCH: Partially update data (alternative to PUT).

    Authentication: Some APIs require authentication via cookies or authorization headers (e.g., JWT). Check API documentation for details.

### Questions:
- First, try to update any city's name to be 'flag'. Then, delete any city. Once done, search for a city named 'flag' to get the flag.
	- HTB{crud_4p!_m4n!pul4t0r}