# Hotel Revenue and Occupancy Analysis Dashboard

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
- **Dataset**: Hotel booking data (anonymized for privacy).

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

![Data Model Screenshot]("")

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
    COUNTROWS(FILTER(fact_bookings, fact_bookings[booking_status] = "Checked Out")), 
    0)
5. **RevPAR [Revenue per Available Room]:**
   ```DAX
  RevPAR = DIVIDE(
    SUM(fact_bookings[revenue_realized]), 
    SUM(fact_aggregated_bookings[capacity]), 
    0)
6. **Occupied_Rooms**
  ```DAX
 Occupied Rooms = COUNTROWS(
    FILTER(fact_bookings, fact_bookings[booking_status] = "Checked Out"))
7. **Occupancy_Rate**
  ``` DAX
    Occupancy Rate (%) = DIVIDE(
    SUM(fact_aggregated_bookings[successful_bookings]), 
    SUM(fact_aggregated_bookings[capacity]), 0) * 100
