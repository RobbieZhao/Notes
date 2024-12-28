## Create tables

    CREATE TABLE IF NOT EXISTS table_name
    (
        column_name PRIMARY KEY,
        column_name REFERENCES table_name (column_name),
        column_name NOT NULL,
    );

## Insert values

    INSERT INTO table_name(column1, column2) VALUES
        (value11, value12),
        (value21, value22);

## Numeric Types

- `serial` autoincrementing integer


## Transaction



To begin a transaction block:
    
    BEGIN;