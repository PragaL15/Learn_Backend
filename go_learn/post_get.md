### Post and get how to write the function

 ###### Why do we need driver?
1.  We need the `driver` is require to interact with the specific database system.
2. Each database has it's own driver as they have unique protocol and their way of handling the queries are different.
3. They also convert the `translation of queries` into `SQL` commands into a format that database understands.
4. Without a driver we need to implement low-level logic for connecting the DB and for sending queries.

##### Setup the database connection

 - You typically have a pre-initialized `*sql.DB` instance (e.g., db), which is used for executing SQL queries. The connection is established during application startup.

 ##### Define the handler function
 1. Parse the incoming request data (usually JSON).
 2. We could validate the data using the `validators`.
- `Validators` -> Validators are tools,library or custom functions used to check that input data meets specific rules or certain constrains.
 They ensure that data is Valid, consistent and safe.
 - It also confrims that data adhere's to domain specific like vaild email format or minimum/maximum length or if the given input is in acceptable range.
  - `go-playground/validator` - This is a custom validation libraries.
  - It could prevent `XXS` - proper validation of user input can reduce risk of injecting malicious scripts.
 3. Construct a SQL `INSERT` Statement and error catch of the inputs are also written.
 4. Excecute the SQL query using `db.Exec` ,It is commonly used for operations such as inserting, updating, deleting data, or executing schema changes like creating or altering tables.
 5. To know the the No.of rows on which the operation gets performed.
 ```go
 lastID, _ := result.LastInsertId()
rowsAffected, _ := result.RowsAffected()
```
- `Syntax Errors`: If the SQL query has syntax issues, db.Exec will return an error.
- `Placeholder Mismatch`: The number of placeholders (?, $1, etc.) in the query must match the number of arguments provided.
- `Connection Issues`: If the database connection is closed or unavailable, db.Exec will fail.
- `Permissions`: Ensure the user has the necessary permissions for the operation.

##### Detailed steps inside the POST Functions

- **Parse the Request Body** 
  - the incomming `HTTP request body` is usually in `JSON format`.
  - Read the body using `r.Body` and decode it into Go struct.
  ```go
  type YourData struct {
    Name  string `json:"name"`
    Email string `json:"email"`
    Age   int    `json:"age"`
   }
  ```
- **Reads the raw body** 
 - `var data struct_name` -> We are storing the data which is expected to be a struct and stores the parsed json data from the request body once it is successfully `decoded`.
 - `err := json.NewDecoder(r.Body).Decode(&data)` -> Reads the raw json body from `r.body` and parses/decode into `data` variable.
 - `r.body` -> Where the client's json payload is stored (Body of `HTTP` request)
 - `json.NewDecoder(r.Body)` -> Creates a JSON decoder that reads directly from `r.body`.
 - `Decode(&data)` -> Parse JSON into the `data` variable.
 - ```go
  if err != nil {
      http.Error(w, "Invalid JSON", http.StatusBadRequest)
      return
  }
  ``` 
  -> Checks if an error occurred during the decoding process.Type Mismatch: If the JSON fields cannot be mapped to the fields of the YourData struct.

- **Construct the SQL Query** -> Create a SQL query string to insert the data into the database.
 - 
 ```sql
 query := "INSERT INTO users (name, email, age) VALUES ($1, $2, $3)"
```
 - Why do we use placeholders ? as `$1 , $2...` to prevent the `sql injection`.

 - **Excecute the Query** -> Use `db.Exec` for simple execution.
  ```go
  _, err = db.Exec(query, data.Name, data.Email, data.Age)
  if err != nil {
      http.Error(w, "Failed to insert data into the database", http.StatusInternalServerError)
      return
  }
  ```
