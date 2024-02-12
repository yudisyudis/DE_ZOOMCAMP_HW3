# DE_ZOOMCAMP_HW3

## This is an explanation about module 3 homework of Data Engineering Zoomcamp which discuss about BigQuery

## Question 1: What is count of records for the 2022 Green Taxi Data??

without need to query, the information about count record can bee seen in:
<img width="522" alt="image" src="https://github.com/yudisyudis/DE_ZOOMCAMP_HW3/assets/91902011/124e8559-67a4-4a3c-ac2f-25f98739d881">

## Question 2 Write a query to count the distinct number of PULocationIDs for the entire dataset on both the tables. What is the estimated amount of data that will be read when this query is executed on the External Table and the Table?

the query we use on external table:
```
SELECT
  DISTINCT PULocationID
FROM
  mage-zoomcamp-yudisyudis.ny_taxi.external_green_taxi_2022;
```

the query we use on internal table:
```
SELECT
  DISTINCT PULocationID
FROM
  mage-zoomcamp-yudisyudis.ny_taxi.green_taxi_2022;
```

## Question 3 How many records have a fare_amount of 0?

```
SELECT
  COUNT(fare_amount)
FROM
  mage-zoomcamp-yudisyudis.ny_taxi.green_taxi_2022
WHERE
  fare_amount = 0;
```

## Question 4 What is the best strategy to make an optimized table in Big Query if your query will always order the results by PUlocationID and filter based on lpep_pickup_datetime? (Create a new table with this strategy)

partition is better use on date formatted data, so the answer is partition by lpep_pickup_datetime, and clustering by PUlocationID. We execute it by this query:

```
CREATE OR REPLACE TABLE mage-zoomcamp-yudisyudis.ny_taxi.green_taxi_cluster_partition
PARTITION BY 
  lpep_pickup_date
CLUSTER BY
  PUlocationID
AS 
SELECT * FROM mage-zoomcamp-yudisyudis.ny_taxi.green_taxi_2022;
```

## Question 5 Write a query to retrieve the distinct PULocationID between lpep_pickup_datetime 06/01/2022 and 06/30/2022 (inclusive). Use the materialized table you created earlier in your from clause and note the estimated bytes. Now change the table in the from clause to the partitioned table you created for question 4 and note the estimated bytes processed. What are these values? 

with non partition table:
```
SELECT
  DISTINCT PULocationID
FROM
  mage-zoomcamp-yudisyudis.ny_taxi.green_taxi_2022
WHERE 
  lpep_pickup_date BETWEEN '2022-06-01' AND '2021-06-30';
```
the answer is:
<img width="1081" alt="image" src="https://github.com/yudisyudis/DE_ZOOMCAMP_HW3/assets/91902011/e7ac1c91-959f-4fe8-9195-fec080874393">

with partition-clustering table:
```
SELECT
  DISTINCT PULocationID
FROM
  mage-zoomcamp-yudisyudis.ny_taxi.green_taxi_cluster_partition
WHERE 
  lpep_pickup_date BETWEEN '2022-06-01' AND '2021-06-30';
```

the answer is:
<img width="1081" alt="image" src="https://github.com/yudisyudis/DE_ZOOMCAMP_HW3/assets/91902011/ef7795c0-0529-4586-9738-c0fa7d65a817">

## Question 6 Where is the data stored in the External Table you created?

The data is located in GCP Bucket

## Question 7 It is best practice in Big Query to always cluster your data

the answer is no

## Questuin 8 No Points: Write a SELECT count(*) query FROM the materialized table you created. How many bytes does it estimate will be read? Why?

the answer is 0 B
<img width="1080" alt="image" src="https://github.com/yudisyudis/DE_ZOOMCAMP_HW3/assets/91902011/e6cb0e7b-e3bc-4828-9def-9bd23a556140">





