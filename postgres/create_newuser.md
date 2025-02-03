To create a new user in PostgreSQL and grant them access to your `medical_records` database, follow these steps:  

---

### **Step 1: Create a New User**  
Run the following command in `psql` to create a new user, replacing `medical_admin` with your desired username:  

```sql
CREATE USER medical_admin WITH PASSWORD 'securepassword';
```

---

### **Step 2: Grant Database Access**  
Now, grant the new user access to the `medical_records` database:  

```sql
GRANT CONNECT ON DATABASE medical_records TO medical_admin;
```

---

### **Step 3: Assign Table Privileges**  
You can grant different levels of access depending on the role of the user:  

#### **Option 1: Read-Only Access (SELECT Only)**
If the user should only be able to view data:  
```sql
GRANT USAGE ON SCHEMA public TO medical_admin;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO medical_admin;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO medical_admin;
```

#### **Option 2: Read & Write Access (SELECT, INSERT, UPDATE, DELETE)**
If the user needs full modification rights:  
```sql
GRANT USAGE ON SCHEMA public TO medical_admin;
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO medical_admin;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO medical_admin;
```

#### **Option 3: Full Ownership (Including Creating and Dropping Tables)**
If the user should have full control over the schema:  
```sql
GRANT ALL PRIVILEGES ON DATABASE medical_records TO medical_admin;
ALTER SCHEMA public OWNER TO medical_admin;
```

---

### **Step 4: Change Ownership of Tables (If Needed)**
If you want `medical_admin` to own the tables instead of `postgres`:  
```sql
ALTER TABLE public.admitted OWNER TO medical_admin;
ALTER TABLE public.api_permissions OWNER TO medical_admin;
ALTER TABLE public.appointments OWNER TO medical_admin;
ALTER TABLE public.doctor_id OWNER TO medical_admin;
ALTER TABLE public.patient_id OWNER TO medical_admin;
ALTER TABLE public.record OWNER TO medical_admin;
ALTER TABLE public.roles OWNER TO medical_admin;
ALTER TABLE public.routes OWNER TO medical_admin;
ALTER TABLE public.user_roles OWNER TO medical_admin;
ALTER TABLE public.user_table OWNER TO medical_admin;
```

---

### **Step 5: Verify Access**
Log in as the new user to check permissions:  
```sh
psql -U medical_admin -d medical_records
```

---

### **Step 6: (Optional) Revoke Unwanted Permissions**
If the user had previous unnecessary permissions:  
```sql
REVOKE ALL PRIVILEGES ON DATABASE medical_records FROM medical_admin;
```
---


## To Grant Permissions to the new role like `Insert` , `Update` , `Delete` and `Sequence`

```sql
-- Grant schema usage (access schema)
GRANT USAGE ON SCHEMA public TO medical_admin;

-- Grant select (view data) and modify privileges (insert, update, delete)
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO medical_admin;

-- Apply these privileges to future tables (new tables created in this schema)
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO medical_admin;

-- Grant usage and select privileges on sequences (auto-increment for IDs)
GRANT USAGE, SELECT ON ALL SEQUENCES IN SCHEMA public TO medical_admin;

-- Apply these privileges to future sequences
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT USAGE, SELECT ON SEQUENCES TO medical_admin;
```
