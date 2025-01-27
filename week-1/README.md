# Module 1 Homework: Docker & SQL

Questions and necessary code when applicable

## Question 1. Understanding docker first run 

```bash
docker run -it --entrypoint /bin/bash python:3.12.8
pip --version
```

## Question 2. Understanding Docker networking and docker-compose

## Question 3. Trip Segmentation Count

```sql
SELECT COUNT(*), 
  CASE
  WHEN trip_distance <= 1 THEN '1'
  WHEN trip_distance <= 3 THEN '2'
  WHEN trip_distance <= 7 THEN '3'
  WHEN trip_distance <= 10 THEN '4'
  ELSE '5' END AS range_group
FROM green_taxi_data
GROUP BY range_group
ORDER BY range_group
```

## Question 4. Longest trip for each day

```sql
SELECT CAST(lpep_pickup_datetime AS DATE) FROM green_taxi_data 
WHERE trip_distance = (
  SELECT Max(trip_distance) from green_taxi_data
)
```

## Question 5. Three biggest pickup zones

```sql
SELECT "Zone" FROM zones where "LocationID" in(
  SELECT "PULocationID" FROM green_taxi_data
  WHERE CAST(lpep_pickup_datetime AS DATE) = '2019-10-18'
  GROUP BY "PULocationID"
  HAVING SUM(total_amount) > 13000
)
```

## Question 6. Largest tip

```sql
SELECT "Zone" FROM zones WHERE "LocationID" = (
	SELECT "DOLocationID" FROM green_taxi_data
	WHERE tip_amount = (
		SELECT MAX(tip_amount) FROM green_taxi_data WHERE "PULocationID" = (
			SELECT "LocationID" FROM zones WHERE "Zone" = 'East Harlem North'
		)
	)
)
```

## Terraform

## Question 7. Terraform Workflow
