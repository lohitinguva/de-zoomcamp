Question#1 

<img width="564" alt="Screenshot 2025-01-27 at 4 46 35 PM" src="https://github.com/user-attachments/assets/e7afd777-fa31-4289-869f-95ea42b45481" />

Question#3

Jupyter Notebook (code)

SQL:

  SELECT
      SUM(CASE WHEN trip_distance <= 1 THEN 1 ELSE 0 END) AS "Up to 1 mile",
      SUM(CASE WHEN trip_distance > 1 AND trip_distance <= 3 THEN 1 ELSE 0 END) AS "1 to 3 miles",
      SUM(CASE WHEN trip_distance > 3 AND trip_distance <= 7 THEN 1 ELSE 0 END) AS "3 to 7 miles",
      SUM(CASE WHEN trip_distance > 7 AND trip_distance <= 10 THEN 1 ELSE 0 END) AS "7 to 10 miles",
      SUM(CASE WHEN trip_distance > 10 THEN 1 ELSE 0 END) AS "Over 10 miles"
  FROM green_tripdata
  WHERE lpep_pickup_datetime >= '2019-10-01'  
  		AND lpep_pickup_datetime < '2019-11-01' 
  		AND lpep_dropoff_datetime < '2019-11-01' 

Question#4

  SQL:

  SELECT
      DATE(lpep_pickup_datetime) AS pickup_date,
      MAX(trip_distance) AS max_trip_distance
  FROM green_tripdata
  WHERE lpep_pickup_datetime >= '2019-10-01' AND lpep_pickup_datetime < '2019-11-01'
  GROUP BY pickup_date
  ORDER BY max_trip_distance DESC
  LIMIT 1

Question#5

  SQL:
  
  SELECT
      zones."Zone" AS pickup_zone,
      SUM(green_tripdata.total_amount) AS total_amount
  FROM green_tripdata
  JOIN zones ON green_tripdata."PULocationID" = zones."LocationID"
  WHERE DATE(green_tripdata.lpep_pickup_datetime) = '2019-10-18'
  GROUP BY zones."Zone"
  HAVING SUM(green_tripdata.total_amount) > 13000
  ORDER BY total_amount DESC

Question#6

  SQL:
  
  SELECT
      dropoff_zones."Zone" AS dropoff_zone,
      MAX(green_tripdata.tip_amount) AS max_tip
  FROM green_tripdata
  JOIN zones AS pickup_zones ON green_tripdata."PULocationID" = pickup_zones."LocationID"
  JOIN zones AS dropoff_zones ON green_tripdata."DOLocationID" = dropoff_zones."LocationID"
  WHERE pickup_zones."Zone" = 'East Harlem North'
    AND DATE(green_tripdata.lpep_pickup_datetime) >= '2019-10-01'
    AND DATE(green_tripdata.lpep_pickup_datetime) < '2019-11-01'
  GROUP BY dropoff_zone
  ORDER BY max_tip DESC
  LIMIT 1

Question#7

terraform init, terraform apply -auto-approve, terraform destroy
