### Datatypes in PostgreSQL
---

### **1. Numeric Data Types**
Used to store numeric values.

| **Type**       | **Description**                        | **Example**       |
|----------------|---------------------------------------|-------------------|
| `SMALLINT`     | 2-byte integer (-32,768 to 32,767)    | `123`             |
| `INTEGER` (or `INT`) | 4-byte integer (-2,147,483,648 to 2,147,483,647) | `10000` |
| `BIGINT`       | 8-byte integer (large range)          | `9223372036854775807` |
| `DECIMAL(p,s)` or `NUMERIC(p,s)` | Exact precision numbers with scale. `p` is precision, `s` is scale. | `NUMERIC(10,2)` stores `12345.67` |
| `REAL`         | 4-byte floating-point number          | `3.14`            |
| `DOUBLE PRECISION` | 8-byte floating-point number      | `3.14159265358979`|

---

### **2. Character Data Types**
Used to store text or string data.

| **Type**          | **Description**                      | **Example**     |
|-------------------|-------------------------------------|-----------------|
| `CHAR(n)` or `CHARACTER(n)` | Fixed-length character (padded with spaces) | `'ABC '` (5-character storage) |
| `VARCHAR(n)` or `CHARACTER VARYING(n)` | Variable-length string with a max length of `n` | `'PostgreSQL'` |
| `TEXT`            | Variable-length text (no limit)     | `'Unlimited Text'` |

---

### **3. Date/Time Data Types**
For storing date and time values.

| **Type**         | **Description**                     | **Example**             |
|------------------|------------------------------------|------------------------|
| `DATE`           | Date (year, month, day)           | `'2024-12-23'`         |
| `TIME`           | Time (hours, minutes, seconds)    | `'14:30:00'`           |
| `TIMESTAMP`      | Date and time (without timezone)  | `'2024-12-23 14:30:00'` |
| `TIMESTAMPTZ`    | Date and time with timezone       | `'2024-12-23 14:30:00+05:30'` |
| `INTERVAL`       | Time interval                    | `'2 days 3 hours'`     |

---

### **4. Boolean Data Type**
Stores true/false values.

| **Type**  | **Description**      | **Example** |
|-----------|----------------------|-------------|
| `BOOLEAN` | True or false values | `TRUE`, `FALSE` |

---

### **5. Array Data Types**
For storing arrays.

| **Type**      | **Description**         | **Example**          |
|---------------|------------------------|----------------------|
| `ARRAY`       | A one-dimensional array of any type | `{1,2,3}` or `{'a','b','c'}` |

---

### **6. JSON Data Types**
For storing JSON-formatted data.

| **Type**  | **Description**                     | **Example**                    |
|-----------|------------------------------------|--------------------------------|
| `JSON`    | Text-based JSON data               | `'{ "key": "value" }'`        |
| `JSONB`   | Binary representation of JSON data | `'{"key": "value"}'`          |

---

### **7. UUID**
For storing universally unique identifiers.

| **Type** | **Description**                          | **Example**                     |
|----------|-----------------------------------------|---------------------------------|
| `UUID`   | 128-bit universally unique identifier   | `'550e8400-e29b-41d4-a716-446655440000'` |

---

### **8. Geometric Data Types**
For storing geometric data.

| **Type**  | **Description**          | **Example**             |
|-----------|-------------------------|-------------------------|
| `POINT`   | Point on a plane        | `(1,2)`                |
| `LINE`    | Infinite line           | `{1,2,3}`              |
| `CIRCLE`  | Circle with a center and radius | `<(1,2),3>`          |

---

### **9. Enumerated Data Types (ENUM)**
Used to define a fixed set of values.

| **Type** | **Description** | **Example** |
|----------|----------------|-------------|
| `ENUM`   | Custom data type | `'sunny'`, `'rainy'`, `'cloudy'` |

---

### **10. Composite Data Types**
Used to define custom structures.

| **Type** | **Description**     | **Example**        |
|----------|--------------------|--------------------|
| `COMPOSITE` | Combine multiple fields | `(1, 'John')` |

---

### **11. Special Data Types**
Unique to PostgreSQL.

| **Type**   | **Description**                     | **Example**       |
|------------|-----------------------------------|-------------------|
| `SERIAL`   | Auto-incrementing integer          | `SERIAL` or `BIGSERIAL` |
| `BYTEA`    | Binary data                        | `E'\\xDEADBEEF'`  |
| `TSVECTOR` | Full-text search                   | `'text search'`   |

---

### Example of Table Creation Using These Data Types
```sql
CREATE TABLE example_table (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    birth_date DATE,
    is_active BOOLEAN,
    scores NUMERIC(5,2)[],
    profile JSONB,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
