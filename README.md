# DE_ZOOMCAMP_HW3

## This is an explanation about module 3 homework of Data Engineering Zoomcamp which discuss about BigQuery

## Question 1: What is count of records for the 2022 Green Taxi Data??

without need to query, the information about count record can bee seen in:
<img width="522" alt="image" src="https://github.com/yudisyudis/DE_ZOOMCAMP_HW3/assets/91902011/124e8559-67a4-4a3c-ac2f-25f98739d881">

## Write a query to count the distinct number of PULocationIDs for the entire dataset on both the tables.
What is the estimated amount of data that will be read when this query is executed on the External Table and the Table?

```
SELECT
  DISTINCT PULocationID
FROM
  mage-zoomcamp-yudisyudis.ny_taxi.green_taxi_2022;
```
