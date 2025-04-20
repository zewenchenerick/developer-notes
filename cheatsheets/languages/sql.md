# SQL Cheat Sheet

## DDL (Data Definition Language)

### SHOW
- **List All Databases**:
    ```sql
    SHOW DATABASES;
    ```

- **Show Current Database**:
    ```sql
    SELECT DATABASE();
    ```

- **Switch to a Database**:
    ```sql
    USE database_name;
    ```

- **List All Tables in the Current Database**:
    ```sql
    SHOW TABLES;
    ```

- **Describe the Structure of a Table**:
    ```sql
    DESCRIBE table_name;
    ```
    Or:
    ```sql
    EXPLAIN table_name;
    ```

- **Show the CREATE Statement for a Table**:
    ```sql
    SHOW CREATE TABLE table_name;
    ```


### CREATE
- **Create a Database**:
    ```sql
    CREATE DATABASE [IF NOT EXISTS] database_name;
    ```

- **Create a Table**:
    ```sql
    CREATE TABLE table_name (
            column1 datatype constraints,
            column2 datatype constraints,
            ...)[comment];
    ```

### CONSTRAINTS
- **Common Constraints**:
    - `NOT NULL`: Ensures a column cannot have a NULL value.
    - `UNIQUE`: Ensures all values in a column are unique.
    - `PRIMARY KEY`: A combination of `NOT NULL` and `UNIQUE`.
    - `FOREIGN KEY`: Links a column to a primary key in another table.
    - `CHECK`: Ensures all values in a column satisfy a condition.
    - `DEFAULT`: Sets a default value for a column.
    - `AUTO_INCREMENT`: Automatically generates a unique value for each new row in a column (commonly used with primary keys).
    - `UNSIGNED`: Ensures a numeric column can only store non-negative values.

### Data Types
#### Numeric Types
| Data Type       | Description                                                                 | Byte Size | Signed Range                          | Unsigned Range                        |
|------------------|-----------------------------------------------------------------------------|-----------|---------------------------------------|---------------------------------------|
| `TINYINT`       | Very small integer data type.                                              | 1 byte    | -128 to 127                           | 0 to 255                              |
| `SMALLINT`      | Integer data type with a smaller range than `INT`.                         | 2 bytes   | -32,768 to 32,767                     | 0 to 65,535                           |
| `MEDIUMINT`     | Integer data type with a range between `SMALLINT` and `INT`.               | 3 bytes   | -8,388,608 to 8,388,607               | 0 to 16,777,215                       |
| `INT`           | Integer data type.                                                         | 4 bytes   | -2,147,483,648 to 2,147,483,647       | 0 to 4,294,967,295                    |
| `BIGINT`        | Integer data type with a larger range than `INT`.                          | 8 bytes   | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | 0 to 18,446,744,073,709,551,615       |
| `DECIMAL(p, s)` | Fixed-point number with precision `p` and scale `s`.                       | Varies    | Depends on precision and scale        | Depends on precision and scale        |
| `NUMERIC(p, s)` | Exact numeric data type with precision `p` and scale `s`.                  | Varies    | Depends on precision and scale        | Depends on precision and scale        |
| `FLOAT`         | Approximate floating-point number.                                         | 4 or 8 bytes | Approximate, depends on implementation | Approximate, depends on implementation |
| `DOUBLE`        | Double-precision floating-point number.                                    | 8 bytes   | Approximate, depends on implementation | Approximate, depends on implementation |

#### String Types
| Data Type       | Description                                                                 | Maximum Size                     | Size Details                       |
|------------------|-----------------------------------------------------------------------------|----------------------------------|------------------------------------|
| `VARCHAR(n)`    | Variable-length string with a maximum length of `n`.                       | Up to 65,535 bytes               | Depends on row size and `n`.       |
| `CHAR(n)`       | Fixed-length string with a length of `n`.                                  | Up to 255 bytes                  | Always uses `n` bytes.            |
| `TEXT`          | Large text data, typically used for storing long strings.                  | 65,535 bytes (64 KB)            | Stored outside the table row.      |
| `TINYTEXT`      | Very small text data, maximum length of 255 characters.                    | 255 bytes                       | Stored outside the table row.      |
| `MEDIUMTEXT`    | Medium-sized text data, maximum length of 16,777,215 characters.           | 16,777,215 bytes (16 MB)        | Stored outside the table row.      |
| `LONGTEXT`      | Large text data, maximum length of 4,294,967,295 characters.               | 4,294,967,295 bytes (4 GB)      | Stored outside the table row.      |
| `ENUM`          | A string object with a predefined set of possible values.                  | 1 or 2 bytes depending on count | Stored as an integer internally.   |

#### Date and Time Types
| Data Type       | Description                                                                 | Size       | Range                                |
|------------------|-----------------------------------------------------------------------------|------------|--------------------------------------|
| `DATE`          | Date value in the format `YYYY-MM-DD`.                                     | 3 bytes    | `1000-01-01` to `9999-12-31`        |
| `DATETIME`      | Date and time value in the format `YYYY-MM-DD HH:MM:SS`.                   | 8 bytes    | `1000-01-01 00:00:00` to `9999-12-31 23:59:59` |
| `TIMESTAMP`     | Date and time value, typically used for tracking changes, in UTC format.   | 4 bytes    | `1970-01-01 00:00:01 UTC` to `2038-01-19 03:14:07 UTC` |
| `TIME`          | Time value in the format `HH:MM:SS`.                                       | 3 bytes    | `-838:59:59` to `838:59:59`         |
| `YEAR`          | Year value in the format `YYYY`.                                           | 1 byte     | `1901` to `2155`                    |

#### Boolean Type
| Data Type       | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| `BOOLEAN`       | Stores `TRUE` or `FALSE` values (often represented as `1` or `0`).         |

#### Binary Types
| Data Type       | Description                                                                 | Maximum Size                     | Notes                                |
|------------------|-----------------------------------------------------------------------------|----------------------------------|--------------------------------------|
| `BLOB`          | Binary large object for storing binary data like images or files.          | 65,535 bytes (64 KB)            | Stored outside the table row.        |
| `TINYBLOB`      | Very small binary object.                                                  | 255 bytes                       | Stored outside the table row.        |
| `MEDIUMBLOB`    | Medium-sized binary object.                                                | 16,777,215 bytes (16 MB)        | Stored outside the table row.        |
| `LONGBLOB`      | Large binary object.                                                      | 4,294,967,295 bytes (4 GB)      | Stored outside the table row.        |

#### Range Types (PostgreSQL Specific)
| Data Type       | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| `RANGE`         | Represents a range of values, often used in PostgreSQL for range types.    |


### Example
```sql
CREATE TABLE employees (
        id INT PRIMARY KEY,
        name VARCHAR(100) NOT NULL,
        age INT CHECK (age >= 18),
        department_id INT,
        FOREIGN KEY (department_id) REFERENCES departments(id)
);
```


### ALTER
- **Add a Column**:
    ```sql
    ALTER TABLE table_name
    ADD column_name datatype constraints;
    ```
- **Modify a Column**:
    ```sql
    ALTER TABLE table_name
    MODIFY column_name new_datatype;
    ```
- **Rename a Column**:
    ```sql
    ALTER TABLE table_name
    RENAME COLUMN old_column_name TO new_column_name;
    ```
- **Rename a Table**:
    ```sql
    ALTER TABLE old_table_name
    RENAME TO new_table_name;
    ```
- **Drop a Column**:
    ```sql
    ALTER TABLE table_name
    DROP COLUMN column_name;
    ```
- **Change a Column** (MySQL-specific):
    ```sql
    ALTER TABLE table_name
    CHANGE old_column_name new_column_name new_datatype;
    ```

### DROP
- **Drop a Database**:
    ```sql
    DROP DATABASE [IF EXISTS] database_name;
    ```
- **Drop a Table**:
    ```sql
    DROP TABLE [IF EXISTS] table_name;
    ```

### TRUNCATE
- **Remove All Data from a Table**:
    ```sql
    TRUNCATE TABLE table_name;
    ```

### RENAME
- **Rename a Table**:
    ```sql
    RENAME TABLE old_table_name TO new_table_name;
    ```



## DML (Data Manipulation Language)

### INSERT
- **Insert Data into a Table**:
    ```sql
    INSERT INTO table_name (column1, column2, ...)
    VALUES (value1, value2, ...), (value1, value2, ...);
    ```

### UPDATE
- **Update Existing Data**:
    ```sql
    UPDATE table_name
    SET column1 = value1, column2 = value2, ...
    [WHERE condition];
    ```

### DELETE
- **Delete Data from a Table**:
    ```sql
    DELETE FROM table_name
    [WHERE condition];
    ```

### Example
```sql
INSERT INTO employees (id, name, age, department_id)
VALUES (1, 'John Doe', 30, 101);

UPDATE employees
SET age = 31
WHERE id = 1;

DELETE FROM employees
WHERE id = 1;
```


## DQL (Data Query Language)
### SELECT
- **Retrieve Data from a Table**:
    ```sql
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition;
    ```