# Service Request Managment Dashboard

### Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiOTljYjMzOWItNDNmYy00ZGVmLWE1NDAtNmVkZDNiNjkyOTI5IiwidCI6ImRmODY3OWNkLWE4MGUtNDVkOC05OWFjLWM4M2VkN2ZmOTVhMCJ9

## Problem Statement

This Dashboard helps in to see the monthly progrees of service request put by customer highlighting ,Daily Avg Request ,giving comparison about prices Vs Quoting and Status of the service request.
It also let us view the Region by amount distribution and service type compariosn.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a Excel file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present.
- Step 5 : In the report view, theme was created based on personal preference inspired by other-levels Youtube channel.
- Step 6 : Since the data contains various categories, thus in order to represent , a new visual multicard was added which tells us about status. 
- Step 7 : Visual filters (Slicers) were added for four fields named "Month".
- Step 8 : one to one model was created between the impoeted data as all sheets had unique value as Request Number
- Step 9 : Started with blank canvas by adding shapes to create the background
- Step 10: Created as mesure table
- Step 11: Created a calclated colmun for month ,year  and quarter to create date hierarchy (made sure  auto time intellignce was off to make the model more faster)
  
                for creating new column following DAX expression was written;
                Quarter = QUARTER(Locations[Date])
                Month = MONTH(Locations[Date])
                Month_F = FORMAT(Locations[Date],"MMM")
  Snap of Calculated Column ,
  
   ![Screenshot 2024-05-02 084106](https://github.com/Samarss3/Service-Request-Dashboard/assets/118118479/172f5b37-e56f-4f8e-aa2b-57dab19cea49)
  

- Step 12: Sorted the month_F column based on Month column
- Step 13: New measure was created to find total count of customers.

Following DAX expression was written for the same,

    Total Daily customer = AVERAGEX(KEEPFILTERS(VALUEs('Locations'[Date])),
              CALCULATE(COUNTA(Locations[Date])))

Snap of measure , 

![Screenshot 2024-05-02 161342](https://github.com/Samarss3/Service-Request-Dashboard/assets/118118479/f12c8af5-dee3-4921-8799-e8683902dba6)

     Avg Daily Request = AVERAGEX(VALUES(Locations[Date]),[Total Daily Request])

Snap of measure , 

![Screenshot 2024-05-02 161752](https://github.com/Samarss3/Service-Request-Dashboard/assets/118118479/3d555c3b-5e3f-4106-a6be-2fa0ab8a345a)



     % paid amount(region) = 
     var total_paid =  SUM(Request_Status[Paid Amount])
    var per = CALCULATE(SUM(Request_Status[Paid Amount]), ALL(Locations[Province]))
    RETURN
    DIVIDE(total_paid,per,0)

Snap of measure , 

![Screenshot 2024-05-02 162254](https://github.com/Samarss3/Service-Request-Dashboard/assets/118118479/10d3cef7-b7a5-43bf-a877-397ca34c4bb0)

    Amount adv = CALCULATE(
    SUM(Request_Status[Paid Amount]),
    Service_Type[Service Type] = "Advertising")

Snap of measure , 

![Screenshot 2024-05-02 162134](https://github.com/Samarss3/Service-Request-Dashboard/assets/118118479/0d8145e8-9084-4399-b909-a8a2f965e79f)

-Step 14: Following Charts were used ,

Snap of Dashboard Overview,

![Screenshot 2024-05-02 162445](https://github.com/Samarss3/Service-Request-Dashboard/assets/118118479/37c83d2d-7c33-49ba-b4cc-2cfb192ad5a2)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.
Following inferences can be drawn from the dashboard;

﻿### [1] **At 89,757.50, Jun had the highest Sum of Paid Amount and was 1,732.16% higher than Nov, which had the lowest Sum of Paid Amount at 4899.**

### [2] Jun accounted for 15.97% of Sum of Paid Amount.
### [3] ﻿Across all 11 Month_F, Count of Request Number ranged from 20 to 167.
### [4] In 4th Quarter Service Request decreased






                     


  


        

 



