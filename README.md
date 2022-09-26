# Sending-vs.-Opening-Snaps
Assume you are given the tables below containing information on Snapchat users, their ages, and their time spent sending and opening snaps. Write a query to obtain a breakdown of the time spent sending vs. opening snaps (as a percentage of total time spent on these activities) for each of the different age groups.

Output the age bucket and percentage of sending and opening snaps. Round the percentages to 2 decimal places.

Notes:

    You should calculate these percentages:
        time sending / (time sending + time opening)
        time opening / (time sending + time opening)
    To avoid integer division in percentages, multiply by 100.0 and not 100.
    
    activities tables : 
|activity_id |user_id	       |activity_type|time_spent|	activity_date|
|------------|---------------|--------------|----------|--------------------|
|7274|	123|	open |  4.50	|06/22/2022 12:00:00
|2425|	123|	send |  3.50	|06/22/2022 12:00:00
|1413|	456|	send |  5.67	|06/23/2022 12:00:00
|1414|	789|	chat |	11.00	|06/25/2022 12:00:00
|2536|	456|	open |	3.00	|06/25/2022 12:00:00



age_breakdown table :
|user_id	|age_bucket
|------------|---------------|
|123 |	31-35
|456 |  26-30
|789 |	21-25

----------------------------------------------------------------------------------------
WITH snaps_statistics AS (
  SELECT 
    age.age_bucket, 
    SUM(CASE WHEN activities.activity_type = 'send' 
      THEN activities.time_spent ELSE 0 END) AS send_timespent, 
    SUM(CASE WHEN activities.activity_type = 'open' 
      THEN activities.time_spent ELSE 0 END) AS open_timespent, 
    SUM(activities.time_spent) AS total_timespent 
  FROM activities
  JOIN age_breakdown AS age 
    ON activities.user_id = age.user_id 
  WHERE activities.activity_type IN ('send', 'open') 
  GROUP BY age.age_bucket) 

SELECT 
  age_bucket, 
  ROUND(100.0 * send_timespent / total_timespent, 2) AS send_perc, 
  ROUND(100.0 * open_timespent / total_timespent, 2) AS open_perc 
FROM snaps_statistics;
