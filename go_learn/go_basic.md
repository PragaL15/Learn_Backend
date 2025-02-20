### Go fibre Basic

1. Why do we need struct in go?

```go
type Request struct {
    UserID            int    `json:"user_id"`
    CardNumber        string `json:"card_number"`
    UpiID             string `json:"upi_id"`
    IFSCCode          string `json:"ifsc_code"`
    AccountNumber     string `json:"account_number"`
    AccountHolderName string `json:"account_holder_name"`
    BankName          string `json:"bank_name"`
    BranchName        string `json:"branch_name"`
    Status            bool   `json:"status"`
}
```
- This struct is used to map the incoming JSON request body.
- Each field corresponds to a specific piece of data (e.g., UserID, CardNumber, etc.) that is expected in the request.
- The json tags specify the name of the `JSON key` that corresponds to each field.

2. Validation is must needed to check the of data sent from frontend is correct and is in same format as out struct else it must throw an error. for that we could use a go library `github.com/go-playground/validator/v10` use `validate` in code.
ex:
```go
  // Initialize the validator
    validate := validator.New()
    // Perform validation
    if err := validate.Struct(req); err != nil {
        return c.Status(fiber.StatusBadRequest).JSON(fiber.Map{"error": err.Error()})
    }
```
The above performs validation.

3. Whenever we are installing an new library from go then we should update `mod` by using `go mod tidy`.

4. Go is designed to `compile directly` into a native binary for the target OS and architecture,You can generate executables for different platforms using `GOOS (Operating System) and GOARCH (Architecture)`.

5. About **serialization**
 - What is serialization?
  Serialization is the process of converting data (Go structs, maps, slices, etc.) into a format that can be stored or transmitted (e.g., JSON, XML, or binary).
  - Why Do We Need Serialization?
To send data over a network (e.g., API responses).
To store structured data in files or databases.
To cache data (e.g., store structs in Redis as JSON).
 -  `Binary serialization` is faster than JSON but not human-readable.

6.  Now if I need to fetch the data from the DB and need it in an API -->
 - The query should have 
    ```sql
            query := "SELECT id, username, email FROM users WHERE id=$1"
            stmt, err := db.DB.Prepare(context.Background(), "get_user", query)
            if err != nil {
                log.Fatal("Failed to prepare statement:", err)
            }
    ```
 - We shoild not use `Select * from table_name` as it fetchs all the column but we need only few column in such cases we must use this.
 
 7. We must use the frequent hits from the DB instead we can use `store frequently accessed data in Redis`.
 - Speeds up API response time by `avoiding DB hits`.

8. Go has it's own **Garbage collection**.This eliminates the need for manual memory management, reducing the likelihood of memory leaks and other bugs that can arise from manual memory management.
9. It's dynamically typed language with the efficiency and safety of a statically typed, compiled language. 

---
**Note**: comipled lang vs interpret language
complied lang -> It's pre compiled into machine code , The development will be slow but excecution will be faster , The compiled executable works only on the OS it was compiled for. 
**ex: golang , c/c++** 
Interprep lang -> interpreted language is executed line by line at runtime by an interpreter , development is faster but excecution will be faster. 
**ex: javascript , python**

---
10. Go is not so object-oriented in the conventional sense , it has no classes but instead we've **structs**.
11. 
