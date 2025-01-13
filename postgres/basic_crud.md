### How to perform a basic CRUD using Stored Procedural

1. Stored Procedure for CRUD Operations.

 ```sql
CREATE OR REPLACE PROCEDURE manage_users(
    op_type TEXT,                     -- Operation type ('INSERT', 'UPDATE', 'DELETE')
    p_user_id INTEGER DEFAULT NULL,   -- User ID (required for update/delete)
    p_user_type_id INTEGER DEFAULT NULL, -- User Type ID
    p_username VARCHAR DEFAULT NULL,  -- Username
    p_password VARCHAR DEFAULT NULL   -- Password
)
LANGUAGE plpgsql
AS $$
BEGIN
    -- Insert Operation
    IF op_type = 'INSERT' THEN
        INSERT INTO users (user_type_id, username, password)
        VALUES (p_user_type_id, p_username, p_password);

    -- Update Operation
    ELSIF op_type = 'UPDATE' THEN
        UPDATE users
        SET 
            user_type_id = COALESCE(p_user_type_id, user_type_id),
            username = COALESCE(p_username, username),
            password = COALESCE(p_password, password)
        WHERE user_id = p_user_id;

    -- Delete Operation
    ELSIF op_type = 'DELETE' THEN
        DELETE FROM users WHERE user_id = p_user_id;

    -- Handle Invalid Operation
    ELSE
        RAISE EXCEPTION 'Invalid operation type: %', op_type;
    END IF;
END;
$$;
```
---
2. Syntax for Calling a Stored Procedure.

```sql
CALL procedure_name(param1, param2, ...);
```
ex: 
- Insert -`CALL manage_users('INSERT', NULL, 1, 'JohnDoe', 'SecurePassword123');`
- Update -`CALL manage_users('UPDATE', NULL, 2, 'UpdatedUser', NULL);`
- Delete -`CALL manage_users('DELETE, 101);`

---

3.  Dropping a Stored Procedure

`DROP PROCEDURE IF EXISTS procedure_name;` - removes the procedure from the db.

---

4. Purpose of COALESCE (Mostly we use this for updating certain fields alone)

```sql
user_type_id = COALESCE(p_user_type_id, user_type_id),
username = COALESCE(p_username, username),
password = COALESCE(p_password, password)
```
1. `p_user_type_id`: The parameter passed to the stored procedure.
2. `user_type_id`: The current value in the database.