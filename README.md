# Sending-vs.-Opening-Snaps
Assume you are given the tables below containing information on Snapchat users, their ages, and their time spent sending and opening snaps. Write a query to obtain a breakdown of the time spent sending vs. opening snaps (as a percentage of total time spent on these activities) for each of the different age groups.

Output the age bucket and percentage of sending and opening snaps. Round the percentages to 2 decimal places.

Notes:

    You should calculate these percentages:
        time sending / (time sending + time opening)
        time opening / (time sending + time opening)
    To avoid integer division in percentages, multiply by 100.0 and not 100.

|------------|---------------|--------------|----------|--------------------|
|activity_id |user_id	       |activity_type|time_spent|	activity_date|
|7274|	123|	open |  4.50	|06/22/2022 12:00:00
|2425|	123|	send |  3.50	|06/22/2022 12:00:00
|1413|	456|	send |  5.67	|06/23/2022 12:00:00
|1414|	789|	chat |	11.00	|06/25/2022 12:00:00
|2536|	456|	open |	3.00	|06/25/2022 12:00:00
