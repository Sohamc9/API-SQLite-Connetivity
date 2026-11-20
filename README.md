# Python SQLite Connectivity Demo

A small Python project showing how to connect to a local SQLite database, create a student table, and insert a student record using Python's built-in `sqlite3` module.

## Features

- Connects to a local `students.db` file
- Creates the `students` table if it does not already exist
- Inserts a sample student using parameterized SQL
- Uses `commit()` to save the change
- Demonstrates both a basic connection flow and an explicitly closed connection

## Requirements

- Python 3
- No third-party packages are required; `sqlite3` is included with Python

## Run the project

Open a terminal in the project folder and run either script:

```bash
python3 sqlconnect.py
```

Or:

```bash
python3 main.py
```

The database file is created in the current working directory if it does not already exist. Run the command from the project folder so it uses the included `students.db` file.

## Project files

| File | Purpose |
|---|---|
| `main.py` | Connects to SQLite, creates the table if needed, inserts one sample student, and commits the change. |
| `sqlconnect.py` | Demonstrates the same operations and explicitly closes the database connection. |
| `students.db` | SQLite database containing the `students` table and sample record. |

## Database schema

The `students` table has these columns:

| Column | Type | Rules |
|---|---|---|
| `id` | `INTEGER` | Primary key; generated automatically |
| `name` | `TEXT` | Required |
| `roll_no` | `TEXT` | Required and unique |
| `marks` | `REAL` | Must be between 0 and 100 |

The sample record inserted by the scripts is:

| Name | Roll number | Marks |
|---|---:|---:|
| Ankit Kulkarni | 39 | 85 |

The insert statement uses `?` placeholders so values are passed separately from the SQL command.

## Expected output

`sqlconnect.py` prints:

```text
Database connected successfully!
Student record added successfully!
Students table created successfully!
```

`main.py` prints the first two lines.

## Note about running it more than once

`roll_no` is unique, and both scripts insert the same sample roll number (`39`). If that record is already in `students.db`, running either script again raises a SQLite unique-constraint error. To try the insert again from a clean database, back up and remove `students.db`; the script will create a new database file on the next run.

## How it works

1. `sqlite3.connect("students.db")` opens the local database (or creates it if it is missing).
2. A cursor runs `CREATE TABLE IF NOT EXISTS` to define the schema.
3. An `INSERT` statement adds the sample row.
4. `connection.commit()` saves the change. `sqlconnect.py` then closes the connection.

