# DVWA SQL Injection (Low Security)

## Project Overview
This project demonstrates a standard SQL Injection (SQLi) attack against the Damn Vulnerable Web App (DVWA) hosted on Metasploitable 2. 
The goal was to manipulate the database query logic to bypass authentication checks and dump the entire user database.

## Environment
* **Attacker:** Kali Linux (Firefox)
* **Target:** Metasploitable 2 (DVWA v1.0.7)
* **Security Level:** Low

## Vulnerability Analysis
The target application is vulnerable because it directly concatenates user input into the SQL query without sanitization or parameterization.

**Vulnerable Code Logic:**
The backend likely executes a query similar to:
`SELECT first_name, last_name FROM users WHERE user_id = '$id';`

## Exploitation
By injecting SQL syntax, the query logic was altered to always return true.

* **Injection Vector:** `%' or '0'='0`
* **Breakdown:**
  * `%`: A wildcard matching any character.
  * `'`: Closes the data field.
  * `or '0'='0`: A tautology (always true statement).
  * The resulting query becomes: `...WHERE user_id = '%' or '0'='0'`

## Result / Proof of Concept
The application responded by returning every record in the user table, confirming the successful injection.

<img width="1289" height="775" alt="sql-injection" src="https://github.com/user-attachments/assets/679277ab-1087-4b65-bfb1-5b08be0a9541" />

## Mitigation
To prevent SQL Injection, the application code should be updated to use:
1. **Prepared Statements (Parameterized Queries):** This separates code from data, ensuring input is never interpreted as SQL commands.
2. **Input Sanitization:** Removing or encoding dangerous characters.
