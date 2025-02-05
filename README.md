# Hotel Revenue and Occupancy Analysis Dashboard
![image alt](https://github.com/Srvskumar/Hotel_Revenue_Analysis/blob/f664b22fd4883fb31d7c5c42dc71cb6eb4cf5b06/Screenshot%202025-02-05%20134846.png)
## Overview
This project is an end-to-end analysis of hotel revenue, occupancy trends, and booking behavior, focusing on actionable insights for optimizing hotel operations. The process involves **data transformation**, **data modeling (Fact Constellation Schema)**, and **visualization** using Power BI, with advanced DAX calculations and an interactive dashboard.

---

## Key Features
1. **Data Preparation**:
   - Extracted raw hotel booking data into Power BI.
   - Performed data cleaning and transformation using Power Query.
2. **Data Modeling**:
   - Implemented a **Fact Constellation Schema** to handle multiple fact tables and shared dimension tables.
   - Optimized the data model for better performance and analysis.
3. **Dashboard Design**:
   - Built an interactive and visually appealing dashboard showcasing:
     - Occupancy trends.
     - Revenue contributions by room type and platforms.
     - Monthly booking and cancellation patterns.

---

## Tools Used
- **Power BI**: Dashboard creation and data visualization.
- **Power Query**: Data transformation and cleaning.
- **DAX Formulas**: Advanced calculations for KPIs and metrics.
- **Dataset**: Hotel booking data 

---

## Data Transformation in Power Query
Data transformation was performed in **Power Query** to clean and prepare the dataset for analysis. The steps include:

1. **Removing Duplicates**:
   - Identified and removed duplicate rows to ensure clean data.

2. **Handling Missing Values**:
   - Replaced null values with appropriate defaults (e.g., `0` for numerical fields, `"Unknown"` for text).

3. **Adding Calculated Columns**:
   - Created custom columns like:
     - `Cancellation Rate = (Cancellations / Total Bookings)`.
     - `Revenue Per Room`.

4. **Data Formatting**:
   - Changed data types (e.g., dates, numerical values) to ensure consistency.

5. **Filtering Data**:
   - Removed outliers and irrelevant data to focus on meaningful insights.

---

## Data Modeling: Fact Constellation Schema
The **Fact Constellation Schema** was used to design the data model. This schema is suitable for complex datasets as it allows multiple fact tables to share common dimension tables, enhancing scalability and flexibility.

### Key Components of the Schema
1. **Fact Tables**:
   - `Bookings Fact Table`: Contains measures like `Total Bookings`, `Revenue`, and `Cancellations`.
   - `Occupancy Fact Table`: Tracks `Occupied Rooms`, `Vacant Rooms`, and `Occupancy Rates`.

2. **Shared Dimension Tables**:
   - `Date Dimension Table`: Provides detailed date-based attributes (e.g., `Month`, `Year`, `Week`).
   - `Customer Dimension Table`: Includes customer demographics and booking behavior.
   - `Room Type Dimension Table`: Details on room categories such as `Luxury`, `Standard`, and `Budget`.

### Advantages of Fact Constellation
- **Flexibility**: Supports analysis across multiple business processes (e.g., occupancy and revenue).
- **Performance Optimization**: Reduces redundancy by sharing dimensions across facts.
- **Enhanced Analysis**: Facilitates complex queries and advanced reporting.

![image alt](https://github.com/Srvskumar/Hotel_Revenue_Analysis/blob/e57eb9b9b56927a78d9b9fec94263b9bdb566f42/Screenshot%202025-02-05%20141236.png)

---
## DAX Formulas
Key DAX formulas used for analysis:

1. **Overall Occupancy Rate**:
   ```DAX
   DIVIDE([Total Rooms Occupied], [Total Available Rooms], 0)
2. **Monthly Cancellation Rate**:
   ```DAX
   DIVIDE([Total Cancellations], [Total Bookings], 0)
3. **Revenue Contribution by Room Type:**
   ```DAX
   DIVIDE(SUMX(FILTER('Bookings', 'Bookings'[Room Type] IN {"Luxury", "Standard"}), 'Bookings'[Revenue]), [Total Revenue], 0)
4. **ADR [Average_Daily_Revenue]**
   ```DAX
   ADR = DIVIDE(
    SUM(fact_bookings[revenue_realized]), 
    COUNTROWS(FILTER(fact_bookings, fact_bookings[booking_status] = "Checked Out")),  0)
5. **RevPAR [Revenue per Available Room]:**
   ```DAX
  RevPAR = DIVIDE(
    SUM(fact_bookings[revenue_realized]), 
    SUM(fact_aggregated_bookings[capacity]), 0)
6. **Occupied_Rooms**
   Occupied Rooms = COUNTROWS(FILTER(fact_bookings, fact_bookings[booking_status] = "Checked Out"))

## Hospitality_Insights
![image alt](https://github.com/Srvskumar/Hotel_Revenue_Analysis/blob/c0207981360bded8e4c648e24f5ed4e4ed775237/Screenshot%202025-02-05%20134829.png)

## INSIGHTS
The analysis revealed the following key findings:

1. **Occupancy Trends**:
   - Luxury rooms consistently achieve higher occupancy rates compared to budget and standard rooms.
   - Weekends and holiday periods show peak occupancy, highlighting opportunities for surge pricing.

2. **Revenue Breakdown**:
   - Direct bookings generate the highest revenue, followed by OTA (Online Travel Agencies) bookings. Promotions can focus on direct booking incentives.
   - Room types contribute unequally to total revenue:
     - **Luxury rooms**: 55% of total revenue.
     - **Standard rooms**: 30%.
     - **Budget rooms**: 15%.

3. **Booking and Cancellation Patterns**:
   - Cancellation rates are highest for OTA bookings, particularly for bookings made more than 30 days in advance.
   - Last-minute bookings (within 7 days) are less likely to be canceled.

4. **Customer Behavior**:
   - Customers booking through direct channels rate satisfaction higher (4.5 average) compared to OTA channels (3.8 average).
   - Guests from higher-income demographics prefer luxury rooms, while budget travelers opt for standard or budget rooms.

5. **Operational Insights**:
   - Rooms remain unoccupied 20% of the time during weekdays, suggesting the need for weekday-specific promotions.
   - Enhancing customer experience for OTA bookings can help reduce cancellations and improve satisfaction.


