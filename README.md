# AMER_Case-Study
SQL Query that analyze the American Energy Market Regulator and identify the providers, outages, emergency status, their reasons and fixing times. 

/* Question 1.1: In the AEMR dataset, write a SQL statement that COUNTS the number of valid (i.e. Status = Approved) outage events for 2016. This should be grouped by and ordered by the outage reason.*/

SELECT 
  COUNT(*) AS Total_Number_Outage_Events, 
  Status, 
  Reason 
FROM AEMR 
WHERE Status = "Approved" AND YEAR(Start_Time) = "2016"
GROUP BY Reason ORDER BY Total_Number_Outage_Events DESC;

/* Write a SQL statement to COUNT the number of valid (i.e. Status = Approved) outage events sorted by their reason (i.e. Forced, Consequential, Scheduled, Opportunistic)* for 2017. */

SELECT 
  COUNT(*) AS Total_Number_Outage_Events, 
  Status, 
  Reason 
FROM AEMR 
WHERE Status = "Approved" AND YEAR(Start_Time) = "2017"
GROUP BY Reason ORDER BY Total_Number_Outage_Events DESC;

/* Write a SQL statement that calculates the average duration in days rounded to 2 decimal places for each approved outage type across both 2016 and */

SELECT
  Status,
  Reason,
  COUNT(*) AS Total_Number_Outage_Events, 
  ROUND(AVG(TIMESTAMPDIFF(MINUTE, Start_Time, End_Time)/1440), 2) AS Average_Outage_Duration_Time_Days, 
  Year
FROM AEMR 
WHERE Status = "Approved" AND Year(Start_Time) = "2016" OR Year(Start_Time) = "2017"
GROUP BY Reason, Year ORDER BY Reason, Year;


