# 🛢️ SQL Fundamentals - TryHackMe Learning Notes

---

## 🧩 Task 1: Introduction

![Database Server Illustration](https://github.com/user-attachments/assets/ffa05183-3b65-440f-b41f-4ed365300022)

Databases are everywhere — from web applications, SOC environments, authentication systems, to malware analysis tools.  
In cybersecurity, both offensive and defensive sides constantly interact with databases.

Databases are crucial for:
- Offensive security (e.g., SQL injection attacks)
- Defensive security (e.g., forensic investigations, suspicious data searches)

### 🎯 Learning Objectives
- Understand databases and core concepts
- Differentiate relational vs. non-relational databases
- Learn SQL CRUD operations
- Use SQL clauses, operators, and functions effectively

---

## 🧩 Task 2: Databases 101


![Relational vs Non-Relational Databases](https://github.com/user-attachments/assets/10f64a60-0ba3-412a-b1b4-bb40409cc391)
![Table Row Column Structure](https://github.com/user-attachments/assets/d87d785b-5d89-4859-b969-aa3728ae54c8)
![Primary Key vs Foreign Key](https://github.com/user-attachments/assets/37f3ef10-6c01-44d9-bc30-fa61c5640073)


### 📚 What is a Database?

A **database** is an organized collection of structured data that can be easily accessed, managed, and updated.

**Real-world examples**:
- Login systems: usernames and passwords
- Social media: posts, comments, likes
- Streaming platforms: watch history and recommendations

---

### 📚 Types of Databases

✔️ **Relational Databases (SQL)**  
- Data stored in tables (rows and columns)
- Consistent structure enforced
- Example: MySQL, PostgreSQL

✔️ **Non-Relational Databases (NoSQL)**  
- Flexible, document-based
- Ideal for varying data formats
- Example (MongoDB document):
```json
{
  "_id": "4556712cd2b2397ce1b47661",
  "name": { "first": "Thomas", "last": "Anderson" },
  "occupation": ["The One"]
}
```

---

### 📚 Tables, Rows, and Columns

- **Table**: Collection of similar records
- **Row**: Single data record
- **Column**: Defines a data type (e.g., Name, Email)

Example Table: `Books`
| id | name | published_date |

---

### 📚 Keys in Databases

- **Primary Key**: Uniquely identifies each record in a table (e.g., `id`)
- **Foreign Key**: Creates relationships between tables (e.g., `author_id` linking `Books` and `Authors`)

---

## 🛢️ Task 3: SQL Overview


![SQL Overview Connection](https://github.com/user-attachments/assets/00950402-322f-4954-9fb3-1dde2f1af29f)
![SQL Security Concepts](https://github.com/user-attachments/assets/f0e6d4eb-6e75-4eb9-9568-0774badf071f)


### 📚 What is SQL?

**SQL (Structured Query Language)** allows us to:
- Create databases and tables
- Insert, update, retrieve, and delete data
- Manage relationships between data

SQL interacts with a **Database Management System (DBMS)** like MySQL or MariaDB.

---

### 📚 Benefits of SQL

✔️ **Speed**: Retrieves huge data sets quickly  
✔️ **Ease of learning**: Plain English style syntax  
✔️ **Accuracy**: Enforces strict structures  
✔️ **Flexibility**: Complex queries easily built

---

### ⚡ Getting Started with MySQL

```bash
mysql -u root -p
# password: tryhackme
```

Success Output Example:
```
Welcome to the MySQL monitor...
Your MySQL connection id is 8
Server version: 8.0.39
```

---

## 🧩 Task 4: Database and Table Statements

### 📚 Managing Databases

- **CREATE DATABASE**
```sql
CREATE DATABASE thm_bookmarket_db;
```
- **SHOW DATABASES**
- **USE database_name**
- **DROP DATABASE database_name**

---

### 📚 Managing Tables

- **CREATE TABLE**
```sql
CREATE TABLE book_inventory (
  book_id INT AUTO_INCREMENT PRIMARY KEY,
  book_name VARCHAR(255) NOT NULL,
  publication_date DATE
);
```

- **SHOW TABLES**
- **DESCRIBE table_name**
- **ALTER TABLE** (Add/Modify Columns)
- **DROP TABLE table_name**

---

## 🛢️ Task 5: CRUD Operations

CRUD = **Create**, **Read**, **Update**, **Delete**

- **INSERT**
```sql
INSERT INTO books (id, name, published_date, description)
VALUES (1, "Android Security Internals", "2014-10-14", "Guide to Android security architecture.");
```

- **SELECT**
```sql
SELECT * FROM books;
SELECT name, description FROM books;
```

- **UPDATE**
```sql
UPDATE books
SET description = "Updated guide on Android Security."
WHERE id = 1;
```

- **DELETE**
```sql
DELETE FROM books WHERE id = 1;
```

---

## 🧩 Task 6: SQL Clauses

✔️ **DISTINCT**
```sql
SELECT DISTINCT name FROM books;
```
(Removes duplicate records)

✔️ **GROUP BY**
```sql
SELECT name, COUNT(*) FROM books GROUP BY name;
```

✔️ **ORDER BY**
```sql
SELECT * FROM books ORDER BY published_date ASC;
```
(Sorting results)

✔️ **HAVING**
```sql
SELECT name, COUNT(*) FROM books GROUP BY name HAVING name LIKE '%Hack%';
```
(Filter grouped results)

---

## 🛢️ Task 7: SQL Operators

✔️ **LIKE**  
```sql
SELECT * FROM books WHERE description LIKE "%guide%";
```
(Search patterns)

✔️ **AND / OR**
```sql
SELECT * FROM books WHERE category = "Offensive" AND name = "Bug Bounty Bootcamp";
```

✔️ **NOT**
```sql
SELECT * FROM books WHERE NOT description LIKE "%guide%";
```

✔️ **BETWEEN**
```sql
SELECT * FROM books WHERE id BETWEEN 2 AND 4;
```

✔️ **Comparison Operators**
- `=`
- `!=`
- `<`, `>`, `<=`, `>=`

---

## 🧩 Task 8: SQL Functions

### 📚 String Functions
- **CONCAT()**
```sql
SELECT CONCAT(name, " - ", category) AS book_info FROM books;
```

- **GROUP_CONCAT()**
```sql
SELECT category, GROUP_CONCAT(name) FROM books GROUP BY category;
```

- **SUBSTRING()**
```sql
SELECT SUBSTRING(published_date, 1, 4) AS year FROM books;
```

- **LENGTH()**
```sql
SELECT LENGTH(name) AS name_length FROM books;
```

---

### 📚 Aggregate Functions
- **COUNT()**
```sql
SELECT COUNT(*) FROM books;
```

- **SUM()**
```sql
SELECT SUM(price) FROM books;
```

- **MAX() / MIN()**
```sql
SELECT MAX(published_date) FROM books;
SELECT MIN(published_date) FROM books;
```

---

## 🛢️ Task 9: Conclusion

🎉 **Congratulations on completing SQL Fundamentals!**

### ✅ Key Takeaways:
- What databases are and why they're critical
- How relational databases structure and relate data
- Basics of SQL querying, inserting, updating, and deleting data
- Using clauses like `GROUP BY`, `ORDER BY`, and functions like `SUM()`, `COUNT()`
- Mastering logical operators and building powerful queries

🚀 These SQL basics are critical skills whether you're investigating, defending, or exploiting data-driven systems in cybersecurity!

---

