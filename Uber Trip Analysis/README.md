# Uber Trip Analysis - Power BI
This project was made using [Data Tutorials](https://www.youtube.com/@datatutorials1) channel.  
   
   Goal: Analyse Uber trip data using Power BI to gain insights into booking trends, revenue, and trip efficiency, 
helping stakeholders make data-driven decisions.
### Dashboard 
https://github.com/user-attachments/assets/dd8c680e-89ad-4466-87e2-84ecf8a5ec6e



## Problem Statement

This dashboard helps to gain insights into booking trends, revenue, and trip efficiency , helping stakeholders to make data- driven decisions.

### Steps followed

- Step 1 : Load data into Power BI Desktop, dataset is a excel workbook file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : Create a Date table and connect the tables as per below snap.
![Snap_1](https://github.com/Sanjeev4318/Power-BI-Projects/blob/main/Snap%201.jpg)
- Step 5 : Add a calculated column Trip Type (Day / Night);

        Trip Type (Day / Night) = 
        VAR HourofDay = HOUR('Trip Details'[Pickup Time])
        RETURN
        IF(HourofDay>=18 || HourofDay<6 ,"Night Trip","Day Trip")

- Step 6 : Add calculated column Pickup Hour (HH MM SS);

        Pickup Hour (HH MM SS) = TIME(HOUR('Trip Details'[Pickup Time]),
        MINUTE('Trip Details'[Pickup Time]),SECOND('Trip Details'[Pickup Time]))
- Step 7 : Add Calculated column Pickup Hour;

      Pickup Hour = HOUR('Trip Details' [Pickup Time])
- Step 8 : Create below KPI's

✓ Total Bookings : Total number of bookings  over a period of time.
✓ Total Booking Value : Total revenue from all the bookings.
✓ Total Trip Distance : Total distance covered by all the trips.
✓ Average Booking Amount : Average revenue per booking.
✓ Average Trip Distance : Average trip distance.
✓ Average Trip time : Average duration of trips.

![Snap 2](https://github.com/Sanjeev4318/Uber-Trip-Analysis-Power-BI/blob/main/Snap%202.jpg)
