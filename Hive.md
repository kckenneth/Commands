# Hive

domains.txt
```
(https://stackoverflow.com/questions/)|(https://www.geeksforgeeks.org/)|(https://www.w3schools.com/)
```

Create DATABASE and TABLE and LOAD 

```
hive> CREATE DATABASE hive_db1 LOCATION '/user/kchen08';
OK
Time taken: 0.134 seconds

hive> CREATE TABLE IF NOT EXISTS hive_db1.domains (urls STRING) LOCATION '/user/kchen08';
OK
Time taken: 0.657 seconds

hive> LOAD DATA INPATH '/user/kchen08/hive/domains.txt' INTO TABLE hive_db1.domains;
Loading data to table hive_db1.domains
OK
Time taken: 1.418 seconds
hive> SELECT * FROM hive_db1.domains
    > 
    > ;
OK
(https://stackoverflow.com/questions/)|(https://www.geeksforgeeks.org/)|(https://www.w3schools.com/)
Time taken: 0.362 seconds, Fetched: 1 row(s)
```
