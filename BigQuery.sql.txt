-- CREATE EXTERNAL TABLE
CREATE OR REPLACE EXTERNAL TABLE
  `arcane-timer-411710.bigQueryHomework.external_green_tripdata`
OPTIONS (
  format = 'parquet', 
  uris = ['gs://aditya_de_zoomcamp_2024_big_query_homework/green_tripdata_2022-*.parquet']
);

-- CREATE Table 
CREATE OR REPLACE TABLE `arcane-timer-411710.bigQueryHomework.green_tripdata`
AS SELECT * FROM `arcane-timer-411710.bigQueryHomework.external_green_tripdata`;

-- Question 1
SELECT COUNT(*) FROM `arcane-timer-411710.bigQueryHomework.external_green_tripdata`;


-- Question 2
SELECT COUNT(DISTINCT(PULocationID)) FROM `arcane-timer-411710.bigQueryHomework.external_green_tripdata`;

SELECT COUNT(DISTINCT(PULocationID)) FROM `arcane-timer-411710.bigQueryHomework.green_tripdata`;

-- Question 3
SELECT COUNT(fare_amount) from `arcane-timer-411710.bigQueryHomework.green_tripdata` where fare_amount = 0;

-- Question 4

CREATE OR REPLACE TABLE `arcane-timer-411710.bigQueryHomework.green_tripdata_partitioned_clustered` 
PARTITION BY DATE(lpep_pickup_datetime)
CLUSTER BY PUlocationID AS 
SELECT * FROM `arcane-timer-411710.bigQueryHomework.green_tripdata`;

-- Question 5
SELECT COUNT(DISTINCT(PUlocationID)) FROM `arcane-timer-411710.bigQueryHomework.green_tripdata_partitioned_clustered` 
where DATE(lpep_pickup_datetime) BETWEEN '2022-06-01' AND '2022-06-30';

SELECT COUNT(DISTINCT(PUlocationID)) FROM `arcane-timer-411710.bigQueryHomework.green_tripdata` 
where DATE(lpep_pickup_datetime) BETWEEN '2022-06-01' AND '2022-06-30';





