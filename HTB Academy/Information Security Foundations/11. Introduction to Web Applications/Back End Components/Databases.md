Web applications utilize back-end databases to store various types of content and information, including:
- **Core Assets**: Images, files, and other essential resources.
- **Application Content**: Posts, updates, and other dynamic content.
- **User Data**: Usernames, passwords, and other personal information.



Databases enable web applications to efficiently store and retrieve data, supporting dynamic content tailored to individual users. Key factors developers consider when choosing a database include:
- **Speed**: Efficiency in data storage and retrieval.
- **Size**: Capacity to handle large volumes of data.
- **Scalability**: Ability to grow with the application.
- **Cost**: Budget considerations for database solutions.



**Types of Databases**
1. **Relational (SQL) Databases**:
    - **Structure**: Data is organized into tables with rows and columns.
    - **Relationships**: Tables can be linked using unique keys, creating relationships between them.
    - **Example**:
        - **Users Table**: Contains columns like `id`, `username`, `first_name`, `last_name`, etc. where `id` serves as the unique key.
        - **Posts Table**: Contains columns like `id`, `user_id`, `date`, `content`, etc., where `user_id` links to the `users` table.


![[web_apps_relational_db.jpg]]

**Relational Databases (SQL)**:
- **Purpose**: Store data in tables with rows and columns, allowing relationships between tables.
- **Schema**: Defines the structure and relationships between tables in the database.



**Example**:
- **Users Table**: Columns include `id`, `username`, `first_name`, `last_name`.
- **Posts Table**: Columns include `id`, `user_id`, `date`, `content`. The `user_id` column links to the `users` table.



**Common Relational Databases**:
- **MySQL**: Open-source, widely used, free of charge.
- **MSSQL**: Microsoft's relational database, used with Windows Servers and IIS.
- **Oracle**: Reliable, used by large businesses, can be costly.
- **PostgreSQL**: Free, open-source, extensible, allows advanced features without major redesign.



**Non-Relational (NoSQL) Databases**:
- **Characteristics**: Do not use tables, rows, columns, or schemas. They are scalable and flexible, ideal for datasets that are not well-defined or structured.



**Storage Models**:
1. **Key-Value**:
    - **Storage**: Stores data as pairs of keys and values.
    - **Example**:
```
{
  "100001": {"date": "01-01-2021", "content": "Welcome to this web application."},
  "100002": {"date": "02-01-2021", "content": "This is the first post on this web app."},
  "100003": {"date": "02-01-2021", "content": "Reminder: Tomorrow is the ..."}
}
```
2. **Document-Based**:
	- **Storage**: Uses complex JSON objects, with metadata and data similar to the Key-Value model.


**Common NoSQL Databases**:
- **MongoDB**: Free, open-source, uses Document-Based model.
- **ElasticSearch**: Free, open-source, optimized for storing and analyzing large datasets.
- **Apache Cassandra**: Free, open-source, highly scalable, handles faulty values gracefully.


**Integration with Web Applications**:
1. **Setup**: Database must be installed and set up on the back-end server.
2. **PHP Example**:
- **Connect to Database**:
```
$conn = new mysqli("localhost", "user", "pass");
```
- **Create Database**:
```
$sql = "CREATE DATABASE database1";
$conn->query($sql);
```
- **Connect to New Database and Query**:
```
$conn = new mysqli("localhost", "user", "pass", "database1");
$query = "SELECT * FROM table_1";
$result = $conn->query($query);
```
- **Search Example**:
```
$searchInput = $_POST['findUser'];
$query = "SELECT * FROM users WHERE name LIKE '%$searchInput%'";
$result = $conn->query($query);
```
- **Display Results**:
```
while($row = $result->fetch_assoc()) {
  echo $row["name"]."<br>";
}
```


**Security Note**: Ensure code is secure to avoid issues like SQL Injection vulnerabilities.


## Questions
- What type of database is Google's Firebase Database?
	- NoSQL