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


querytest 

Without LIMIT, it crashes 

```
SELECT 
    a.page_search_term, a.view_id, 
    SUM(CASE WHEN (a.qtypeAgg = "1") THEN 1 ELSE 0 END) AS clicks,
    SUM(CASE WHEN (a.qtypeAgg = "3") THEN 1 ELSE 0 END) AS reformulate,
    SUM(CASE WHEN (a.qtypeAgg = "0") THEN 1 ELSE 0 END) AS abandonment,
    SUM(CASE WHEN (a.targurls RLIKE 'https://stackoverflow.com') THEN 1 ELSE 0 END) AS SO,
    SUM(CASE WHEN (a.targurls RLIKE 'https://www.geeksforgeeks.org') THEN 1 ELSE 0 END) AS GFG,
    SUM(CASE WHEN (a.targurls RLIKE 'https://www.w3schools.com') THEN 1 ELSE 0 END) AS W3S
FROM (
SELECT
    page_search_term, view_id, qtypeAgg, vi['targurl'] AS targurls
FROM
    maw_gdpr.fact_search_nonbot_daily lateral view explode(view_info) vit as vi
WHERE
    dt >= '20230101'
    AND dt <= '20230131'
    AND platform = 'pc'
    AND market = 'us'
    AND vertical = 'websearch'
    AND event_trigger IN ('view','click')
    AND page_info['pagenum'] = 1
    AND page_info['mtestid'] RLIKE '{BUCKET}'
    AND page_info['ddb'] RLIKE '{MODULE}'
    AND view_info is not null 
    AND CAST(vi['pos'] AS INT) BETWEEN 1 and 5
    AND vi['targurl'] is not null
    AND vi['t4'] = 'title'
    AND vi['sec'] = 'sr'
LIMIT 300000
) a 
GROUP BY page_search_term, view_id
```

