1. 
```sql
CREATE OR REPLACE FUNCTION update_updated_at_column()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updatedAt = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
- **Function declaration** it creates a function - CREATE OR REPLACE FUNCTION 
- **Function name**  - update_updated_at_column()
- **Function return statement** - RETURNS TRIGGER AS $$
   `TRIGGER` - The function is designed to be invoked automatically in response to a trigger event, such as an UPDATE on a table.
- **Trigger logic** - 
```sql
BEGIN
    NEW.updatedAt = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
```
- BEGIN and END these blocks will contain the logic that will be executed when the trigger fires
- `NEW` -  It represents the row after the change is applied or if any new action is performed.
 here `updatedAt` is field in DB that need to be updated after trigger fires.
 `CURRENT_TIMESTAMP` This function returns the current date and time based on the server’s clock.
 Now, the `updatedAt` will have the updated time.
- `RETURN NEW` - Without returning the new the changes made in above code will be ignored.

2. `$$ LANGUAGE plpgsql;` - 
  - `$$`: These are delimiter markers that mark the start and end of the function's body in PostgreSQL. 
  - The double dollar signs ($$) are often used when defining functions, as they allow you to avoid escaping special characters (such as single quotes) inside the function body.

`LANGUAGE plpgsql`: This specifies the language used for the function. In this case, plpgsql is the procedural language used in PostgreSQL for writing trigger functions, which allows for procedural logic like conditionals, loops, and variables.

---

2. Creating a trigger function in table

```sql
CREATE TRIGGER set_updated_at
BEFORE UPDATE ON course_table
FOR EACH ROW
EXECUTE FUNCTION update_updated_at_column();
```
**CREATE TRIGGER** - This is the command used to create a new trigger in PostgreSQL
set_updated_at --> trigger name
**BEFORE** - The trigger fires before the row is actually updated.
**UPADTE** - The event that triggers the function.
**ON course_table** - this will say on which table these operations must takeplace.
**FOR EACH ROW** - This will ensure that trigger fires when each row is actually updated. --> This is called 
`Row-Level Trigger` as it's looking on each row.
 - if we us `FOR EACH STATEMENT`, the trigger would fire only once for the entire update statement, regardless of how many rows are affected.

**EXECUTE FUNCTION**functn_name - This will excecute the function which we wrote using logics.

---

