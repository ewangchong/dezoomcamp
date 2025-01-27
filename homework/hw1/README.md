# dezoomcamp
## Question 1:
pip -V
## Question 2:
N/A
## Question 3:
~~~sql
SELECT
	CASE
		WHEN TRIP_DISTANCE <= 1 THEN 'up to 1 mile'
		WHEN TRIP_DISTANCE > 1 AND TRIP_DISTANCE <= 3 THEN '1 to 3 miles'
		WHEN TRIP_DISTANCE > 3 AND TRIP_DISTANCE <= 7 THEN '3 to 7 miles'
		WHEN TRIP_DISTANCE > 7 AND TRIP_DISTANCE <= 10 THEN '7 to 10 miles'
		ELSE 'Over 10 miles'
	END AS DISTANCE_CATEGORY,
	COUNT(*) AS TRIP_COUNT
FROM
	GREEN_TAXI_DATA
WHERE
	LPEP_PICKUP_DATETIME >= '2019-10-01'
	AND LPEP_DROPOFF_DATETIME < '2019-11-01'
GROUP BY
	DISTANCE_CATEGORY
~~~
## Question 4:
~~~sql
WITH daily_max_distance AS (
    SELECT
        DATE(lpep_pickup_datetime) AS pickup_day,
        MAX(trip_distance) AS max_distance
    FROM
        public.green_taxi_data
    GROUP BY
        DATE(lpep_pickup_datetime)
)
SELECT
    pickup_day,
    max_distance
FROM
    daily_max_distance
ORDER BY
    max_distance DESC
LIMIT 1;
~~~
## Question 5:
~~~sql
SELECT
    z."Borough",
    z."Zone",
    SUM(g.total_amount) AS total_amount
FROM
    public.green_taxi_data g
JOIN
    public.zones z ON g."PULocationID" = z."LocationID"
WHERE
    DATE(g.lpep_pickup_datetime) = '2019-10-18'
GROUP BY
    z."Borough", z."Zone"
HAVING
    SUM(g.total_amount) > 13000
ORDER BY
    total_amount DESC;
~~~
## Question 6:
~~~sql
SELECT
    dz."Zone" AS dropoff_zone,
    g.tip_amount AS tip
FROM
    public.green_taxi_data g
JOIN
    public.zones pz ON g."PULocationID" = pz."LocationID"
JOIN
    public.zones dz ON g."DOLocationID" = dz."LocationID"
WHERE
    pz."Zone" = 'East Harlem North'
    AND g.lpep_pickup_datetime >= '2019-10-01'
	AND g.lpep_pickup_datetime < '2019-11-01'
ORDER BY
    g.tip_amount DESC
LIMIT 1
~~~
## Question 7:
N/A
