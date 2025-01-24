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
---
3. Whenever we are installing an new library from go then we should update `mod` by using `go mod tidy`.

4. 