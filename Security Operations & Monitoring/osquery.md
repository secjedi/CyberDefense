Osquery is an opensource tool used to query an endpoint (multiple endpoints) using SQL syntax.
Found in Alienvault and Cisco AMP.
Fisrt command `osqueryi`
This opens up and interactive sql-like shell

`.tables process` list available tables  that has the word proccess table in it
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/osquery/7.png) <br />

We need to query tables, we should find the table schema

`.schema table_name`
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/osquery/8.png) <br />

Looking at the above image, pid is the column, and BIGINT is the type. 





