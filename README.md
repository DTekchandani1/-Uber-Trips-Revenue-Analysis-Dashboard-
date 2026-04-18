🚖 Uber Trips & Revenue Analysis Dashboard (Power BI)
1.  Project Overview
This project presents an interactive Power BI dashboard built to analyze ride-sharing data from Uber.
The dashboard provides insights into rider behavior, revenue trends, vehicle performance, and customer patterns across multiple dimensions.
It is designed with a business-focused approach, enabling stakeholders to make data-driven decisions.

2.   Objectives
	Analyze booking trends (monthly & quarterly)
	Track revenue performance
	Evaluate vehicle category performance
	Understand customer behavior & retention
	Identify cancellation patterns
	Compare payment methods usage
3.   Dashboard Features
	  Home Page
Clean landing page with navigation Modern UI inspired by Uber branding Easy access to all dashboard sections.

	  Overview Dashboard

	📌 Key Metrics (Overview Dashboard)
•	Total Bookings: 93K 
•	Revenue: 52M 
•	Lost Bookings: 57K 
•	Average Distance: 24.64 km 
•	Total Distance: 2.51M km 
	📅 Time-Based Insights
•	January has the highest monthly bookings (8,189) 
•	Q2 is the strongest quarter (23,268 bookings) 
•	March generates the highest revenue (4.6M) 
•	Peak booking time: 6 PM – 9 PM 
	💳 Payment Insights
•	UPI is the dominant payment method: 
o	Revenue: 23M+ 
o	Highest number of paying customers: 41K 
	  Vehicle Analysis

Vehicle Type	Total Bookings	Revenue	Customers	Cont%
Auto	23,128	12.8M	32,948	100%
Bike	20,560	11.4M	29,138	100%
Go Mini	18,529	10.3M	28,358	100%
Go Sedan	16,666	9.3M	23,330	100%
Premier Sedan	11,247	6.2M	16,827	100%
Uber XL	2,783	1.5M	4,447	100%
	📌 Insight:
•	Auto and Bike dominate volume and revenue 
•	Uber XL has the lowest demand → niche usage 
•	Trend indicators using sparklines
	  Revenue Dashboard

	Revenue is 4.57M in march month is highest
	Revenue is 13.07M in 1St Quarter is highest
	Revenue by Auto is 13M
	Revenue by UPI is 23.3M
	Revenue by Customer_id C7828101 is 7.7K

	  Rider Analysis

	👤 Customer Insights
•	Total customers: 104K+ (monthly/quarterly aggregated view) 
•	Customer Rating: 4.40 
•	Driver Rating: 4.23 
	Rider Segments
•	First-time riders 
•	Return riders 
•	Regular riders (3+ trips) 
📌 Example High-Value Customer:
•	Customer ID C7828101 
o	Revenue: 7,683 
o	Avg Distance: 31.09 km 
	⚠️ Operational Issues
•	Customer-related issues: 6,835 
•	Over-capacity riders: 6,684 
•	Personal vehicle issues: 6,724 
•	Sick passenger reports: 6,751 
•	Missing/blank booking records: 29,942 ⚠️ 
📌 Insight:
High number of blank/issue records indicates data quality or operational gaps
	  Location Insights (if included)
•	Top Pickup Location: Khandsa (~600+ bookings) 
•	Top Drop Location: Ashram (~592 bookings) 
•	Busiest Location: Khandsa (~949 bookings) 
📌 Distance Trends:
•	January distance: 222K km 
•	Q4 highest distance: 630K km 
•	Auto contributes highest distance: 0.63M km 
	⏰ Time Slot Analysis
•	Peak slot: 6 PM – 9 PM 
•	Highest demand consistently across all weekdays 
📌 Insight:
Evening hours drive the majority of revenue → commuter + leisure demand
4.  Tools & Technologies
•	Microsoft Power BI Desktop 
•	DAX (Data Analysis Expressions) 
•	Data Modeling 
•	Interactive dashboards (Bookmarks, Filters, Drilldowns) 
5.🧠 Key DAX Measures Used
Booking _Count=DISTINCTCOUNT(Uber[Booking ID])

Completed_Booking=CALCULATE([Booking _Count],Uber[Booking Status]="Completed")

Lost_Booking=CALCULATE([Booking _Count],Uber[Booking Status]<>"Completed")

Booking_Value=SUM(Uber[Booking Value])

Total_Distance=SUM(Uber[Ride Distance])

Calender=SUMMARIZE(Uber,Uber[Date])

Month=FORMAT(Calender[Date],"mmm")

Month_Index=MONTH(Calender[Date])

Quarter="Q"&QUARTER(Calender[Date]) 

Quarter_Index=QUARTER(Calender[Date])

Booking_Remove_Status_Filter = CALCULATE([Booking _Count],ALL(Uber[Booking Status]))

AVG_Distance=AVERAGE(Uber[Ride Distance])

Customer_count=DISTINCTCOUNT(Uber[Customer ID])

Cont% = VAR Vehicle_Remove_filter=CALCULATE([Booking_Value],ALL(Uber[Ve_Type])) VAR Revenue=[Booking_Value] RETURN DIVIDE(Revenue,Vehicle_Remove_filter)

First_Time = COUNTROWS(FILTER(SUMMARIZE(Uber,Uber[Customer ID],"Count",COUNT(Uber[Booking ID])),[Count]=1))

Return_Rider = COUNTROWS(FILTER(SUMMARIZE(Uber,Uber[Customer ID],"Count",COUNT(Uber[Booking ID])),[Count]=2))

Regular_Rider = COUNTROWS(FILTER(SUMMARIZE(Uber,Uber[Customer ID],"Count",COUNT(Uber[Booking ID])),[Count]>=3))

Time_Slot = 
VAR _hour = HOUR(Uber[Time])
RETURN 
SWITCH(
    TRUE(),
    _hour >= 9 && _hour < 12, "09AM-12PM",
    _hour >= 12 && _hour < 15, "12PM-03PM",
    _hour >= 15 && _hour < 18, "03PM-06PM",
    _hour >= 18 && _hour < 21, "06PM-09PM",
    _hour >= 21 && _hour < 24, "09PM-12AM",
    _hour >= 0 && _hour < 3,  "12AM-03AM",
    _hour >= 3 && _hour < 6,  "03AM-06AM",
    _hour >= 6 && _hour < 9,  "06AM-09AM",
    "Blank"
)

Time_Slot_Sort = 
SWITCH(
    TRUE(),
    HOUR(Uber[Time]) >= 0 && HOUR(Uber[Time]) < 3, 1,
    HOUR(Uber[Time]) >= 3 && HOUR(Uber[Time]) < 6, 2,
    HOUR(Uber[Time]) >= 6 && HOUR(Uber[Time]) < 9, 3,
    HOUR(Uber[Time]) >= 9 && HOUR(Uber[Time]) < 12, 4,
    HOUR(Uber[Time]) >= 12 && HOUR(Uber[Time]) < 15, 5,
    HOUR(Uber[Time]) >= 15 && HOUR(Uber[Time]) < 18, 6,
    HOUR(Uber[Time]) >= 18 && HOUR(Uber[Time]) < 21, 7,
    HOUR(Uber[Time]) >= 21 && HOUR(Uber[Time]) < 24, 8
)

Weekday_Index = WEEKDAY(Calender[Date], 1)

Weekday = FORMAT(Calender[Date],"ddd")

6.   Dataset
Simulated / sample Uber ride dataset
Includes:
Trip details
Customer data
Vehicle types
Payment methods
Location data

7.   Key Insights
UPI dominates as the most used payment method Auto & Bike categories contribute highest bookingsRevenue remains consistent with slight monthly fluctuations
High number of repeat customers indicates retention strength Cancellations & incomplete rides highlight operational gaps

8.   Business Recommendations
	Reduce Lost Bookings (57K ⚠️)
•	Improve driver availability during peak hours 
•	Introduce dynamic pricing incentives 
•	Optimize ride allocation algorithm 

	Focus on High-Demand Time Slots
•	Increase driver supply during 6 PM – 9 PM 
•	Offer surge incentives for drivers in peak hours 

	Strengthen UPI Ecosystem
•	Promote cashback/offers on UPI 
•	Partner with payment providers to increase retention 

	Expand in High-Performing Locations
•	Increase driver density in Khandsa & Ashram 
•	Use geo-targeted promotions 

	Improve Data Quality
•	Investigate 29K blank booking records 
•	Implement validation checks in data pipeline 

	Optimize Vehicle Mix
•	Increase Auto & Bike supply (high demand) 
•	Re-evaluate Uber XL positioning (low usage) 
	Customer Experience Improvements
•	Address frequent complaints (overcrowding, hygiene) 
•	Introduce driver quality monitoring system 

9.  How to Use
	Download the .pbix file from this repository
	Open in Power BI Desktop
	Interact with filters, slicers, and visuals

10.  Dashboard Preview
        ![Dashboard Preview](images/dashboard.png)
11. 🚀 Conclusion
This dashboard provides a 360° view of Uber operations, highlighting:
•	Revenue drivers 
•	Customer behavior 
•	Operational inefficiencies 
It enables stakeholders to make data-driven decisions to improve efficiency, revenue, and customer satisfaction.
  Contact

Deepak Kumar Tekchandani
 Power BI|DAX (Data Analysis Expressions)|Data Modeling|Data Cleaning & Transformation|Interactive Data Visualization

📧 deepakkumartekchandani@gmail.com  
🔗 LinkedIn: www.linkedin.com/in/deepak-kumar-tekchandani-b7200a146
💻 GitHub: https://github.com/DTekchandani1/-Uber-Trips-Revenue-Analysis-Dashboard-.git













