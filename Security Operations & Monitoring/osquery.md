Osquery is an opensource tool used to query an endpoint (multiple endpoints) using SQL syntax.
Found in Alienvault and Cisco AMP.
Fisrt command `osqueryi`
This opens up and interactive sql-like shell
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/osquery/7.png) <br />

`.tables process` list available tables  that has the word proccess table in it. <br />
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/osquery/8.png) <br />

We need to query tables, we should find the table schema

`.schema table_name`
![alt text](https://github.com/secjedi/CyberDefense/blob/main/Images/osquery/9.png) <br />

Looking at the above image, pid is the column, and BIGINT is the type. 

If we need to check schema for another OS, we will need to use `--enable_foreign` command line flag
More command_line flag here: https://osquery.readthedocs.io/en/latest/installation/cli-flags/ <br />








