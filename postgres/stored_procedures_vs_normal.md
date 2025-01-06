### **Advantages of stored procedures**

1. **Reusable Logic:**
   - The procedure handles all operations (`INSERT`, `UPDATE`, `DELETE`) using a single reusable function.
2. **Reduced Complexity:**
   - Default values (like `CURRENT_TIMESTAMP`) and optional parameters (e.g., `NULL` values) are handled inside the procedure.
3. **Validation:**
   - The procedure ensures only valid operations (`INSERT`, `UPDATE`, `DELETE`) are executed.
4. **Security:**
   - The procedure protects against SQL injection by encapsulating raw SQL within the database.

---
### Normal query vs stored procedures

| Feature                          | **Normal Query**                                   | **Stored Procedure**                           |
|----------------------------------|---------------------------------------------------|------------------------------------------------|
| **Code Reusability**             | Low: Queries must be written for each operation   | High: Centralized logic for all operations    |
| **Performance**                  | Slower: Queries are re-parsed each time           | Faster: Precompiled and cached by PostgreSQL  |
| **Security**                     | Vulnerable if queries are improperly sanitized    | Secure: SQL injection risk minimized          |
| **Maintenance**                  | Tedious: Changes must be made in multiple places | Easy: Update logic in one place               |
| **Complexity**                   | Higher: Repeated handling of default values       | Lower: Default values handled in procedure    |
| **Error Handling**               | Must be implemented in every query               | Centralized in the procedure                  |
| **Validation**                   | Manual validation in every query                 | Handled in one place in the procedure         |

---
