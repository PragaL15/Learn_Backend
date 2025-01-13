### What is SQL Injection?

SQL Injection is a type of security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. By injecting malicious SQL code, attackers can:

1. **Bypass Authentication:** Gain unauthorized access to accounts or systems.
2. **Manipulate Data:** Read, modify, insert, or delete data in the database.
3. **Execute Administrative Operations:** Execute database administration commands.
4. **Expose Sensitive Data:** Extract confidential information such as passwords or credit card details.
5. **Destroy Database Integrity:** Delete or corrupt data.

SQL Injection occurs when user-provided input is not properly sanitized and directly concatenated into SQL queries. For example:

```sql
SELECT * FROM users WHERE username = 'user_input' AND password = 'user_input';
```
If an attacker inputs something like:

```sql
' OR '1'='1
```
The query becomes:

```sql
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = '' OR '1'='1';
```

This condition always evaluates to true, allowing unauthorized access.

---

### How to Prevent SQL Injection

1. **Use Stored Procedures:**
   Stored procedures can encapsulate SQL logic on the database side, reducing the risk of injection.

   **Example:**
   ```sql
   CREATE PROCEDURE GetUser(IN username VARCHAR(255), IN password VARCHAR(255))
   BEGIN
       SELECT * FROM users WHERE username = username AND password = password;
   END;
   ```
   ---
   