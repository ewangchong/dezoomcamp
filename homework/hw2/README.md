# dezoomcamp
## Question 1:
128.3MB
## Question 2:
green_tripdata_2020-04.csv
## Question 3:
~~~sql
SELECT
	COUNT(*)
FROM
	PUBLIC.YELLOW_TRIPDATA
WHERE FILENAME like 'yellow_tripdata_2020%'
~~~
## Question 4:
~~~sql
SELECT
	COUNT(*)
FROM
	PUBLIC.GREEN_TRIPDATA
WHERE FILENAME like 'green_tripdata_2020%'
~~~
## Question 5:
~~~sql
SELECT
	COUNT(*)
FROM
	PUBLIC.YELLOW_TRIPDATA
WHERE FILENAME like 'yellow_tripdata_2021-03%'
~~~
## Question 6:
~~~yaml
triggers:
  - id: daily
    type: io.kestra.plugin.core.trigger.Schedule
    cron: "@daily"
    timezone: America/New_York
~~~
