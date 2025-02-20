CREATE OR REPLACE EXTERNAL TABLE `hw3.yellow_taxi_trips_external`
OPTIONS (
    format = 'PARQUET',
    uris = ['gs://dezoomcamp_hw3_2025_bob_va_1/yellow_tripdata_2024-*.parquet']
);

CREATE MATERIALIZED VIEW `hw3.yellow_taxi_trips_mv`
AS
SELECT * FROM `hw3.yellow_taxi_trips`;

SELECT COUNT(*)
FROM `hw3.yellow_taxi_trips_external`
where fare_amount = 0

CREATE OR REPLACE TABLE `hw3.optimized_yellow_taxi_trips`
PARTITION BY DATE(tpep_dropoff_datetime)  -- Partitioning by dropoff date
CLUSTER BY VendorID                       -- Clustering by VendorID
AS
SELECT *
FROM `hw3.yellow_taxi_trips`;

SELECT DISTINCT VendorID
FROM `hw3.yellow_taxi_trips`
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' AND '2024-03-15';

