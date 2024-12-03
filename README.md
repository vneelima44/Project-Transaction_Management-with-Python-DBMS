# Product Insertion to PostgreSQL

This Python script demonstrates how to interact with a PostgreSQL database to insert a product into a `product` table. The script handles transaction management, error handling, and ensures that the insertion only happens if no conflicts occur (i.e., no duplicate `prod_id`).

## Features

- Establishes a connection to a PostgreSQL database.
- Inserts a new product into the `product` table.
- Handles any conflicts (duplicate `prod_id`) using the `ON CONFLICT DO NOTHING` clause.
- Uses **transactions** to ensure data consistency.
- Implements **error handling** with rollback capabilities in case of failure.
- **Commits** changes to the database to make them permanent.
- Properly **closes** the database connection to release resources.

## Requirements

- Python 3.x
- PostgreSQL 9.5+ (or any version that supports `ON CONFLICT` clause)
- `psycopg2-binary` Python library for PostgreSQL database interaction.

### Installation of Python dependencies

To install the necessary Python dependencies, run:

```bash
pip install psycopg2-binary==2.9.3
Setup

Ensure that you have PostgreSQL installed and running on your system.
Create a database named postgres (or modify the code to use your existing database).
Create a table called product with the following schema (if it doesn't already exist):
CREATE TABLE product (
    prod_id VARCHAR(20) PRIMARY KEY,
    pname VARCHAR(50),
    price DECIMAL
);
Adjust the database connection parameters in the code to match your environment:
Replace the host, database, user, and password in the connection string with the appropriate values.

Code Walkthrough

1. Connection Setup
The script connects to the PostgreSQL database using the psycopg2 library.
It uses the localhost for the database server, but this can be adjusted to any remote server.
2. Transaction Management
Autocommit is disabled, ensuring that all SQL statements are executed as part of a single transaction.
If an error occurs, the script rolls back the transaction to ensure no partial changes are saved.
3. Insert Data
The script attempts to insert a product into the product table.
It uses the ON CONFLICT (prod_id) DO NOTHING clause to prevent duplicate prod_id entries from being inserted.
After executing the insert statement, the transaction is committed to make the changes permanent.
4. Error Handling
If any exception or database error occurs during execution, the script prints the error message and rolls back the transaction to ensure the database is not in an inconsistent state.
5. Closing the Connection
The cursor and database connection are properly closed in the finally block to ensure that resources are released.
