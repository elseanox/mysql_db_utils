mysql_db_utils
==============
MySQL DB Utilities for Meep Freak

This directory contains a number of linux/unix utilities to ease MySQL/Linux administration.

p - Dumps essential full processlist and show engine innodb status output to the files proc.out and inno.out. p backs up previous versions with a timestamp. 

Sorting the processlist using './p | sort -nr -k 6' will give you a reverse sort of all queries by execution time. 

Grepping inno.out like this 'grep TRANSACTION inno.out' will give you a stack output of all the innodb transaction thread ids. The bottom of stack is the 'oldest' or rather a 'long running' query that may be a blocker.

  invocation - ./p (you will be prompted for the root mysql password if $PASS is unset)



db_canary_query - Pings a mysql server with the query of your choice. Writes to a log. Alerts if pingtime is over threshold. Signals unexpected swapping or virtual machine resource weather issues.

  invocation example: nohup <path>/db_canary_query & (runs for a week)
  cron example: 0 0 * * 6 <path>/db_canary_query 



eth_to_serverid - concocts a pseudo-unique server id for mysql replication based on the outbound eth or bond address

  invocation example: eth_to_serverid

  returns something like: 100215



long_query_alarm - emails an address of your choice with the worst offending query that is executing longer than LONG_QUERY_TIME

  invoication example: long_query_alarm

  returns an email containing: mysql query thread id, execution time, query string
  


schema_size_report - returns the size of all schemas on a mysql instance (omits mysql, information_schema and performance_schema)

  invocation example: ./schema_size_report  

  returns a formatted list of schemas and their size in megabytes
  
  

host_port_ping - checks for the presence of a demon running at host:port reports on fail to an email address, 60 second interval

  invocation example: ./host_port_pint 10.0.0.2 3306 someone@email.com
  
  returns success or email spew on failure
