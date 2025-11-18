# Quality Control Dashboard

![Quality_Control_Dashboard.PNG](/Resources/Images/Quality_Control_Dashboard.gif)

## Introduction

This interactive dashboard tracks defect trends and repair costs over a 6-month period, providing insights to guide quality improvement decisions.

The dataset was sourced from Kaggle and includes manufacturing defect records, detailing Defect type, Defect Location, Severity, Inspection Method, and associated Repair Costs.
The Raw Dataset is in [defects_data.csv](/Resources/Dataset/defects_data.csv)

### Dashboard File
My final dashboard is in [Quality_Control_Dashboard.xlsx](Quality_Control_Dashboard.xlsx).

### Excel Skills Used
- **📊 Charts and Pivot Tables**
- **🧮 Functions and Formulas**
- **📋 Slicers and Filters**

### Data Jobs Dataset
This dataset comprises 6-months of records on manufacturing defects, capturing key details on ...

- **🧩 Defect Location (Component, Internal, Surface)**
- **🛠️ Defect Type (Cosmetic, Functional, Structural)**
- **🔴 Severity (Critical, Moderate, Minor)**
- **🔍 Inspection Method (Automated, Manual, Visual)** 
- **💰 Repair Cost**

## Dashboard Build

### 📉 Charts and Pivot Tables
#### (1) Defects Per Month - Area Chart

<img src="/Resources/Images/Area_Chart.PNG" width="850" height="550" alt="Area_Chart1.PNG">

- 🛠️ **Excel Features:** Area chart that visualizes defect quantities over a 6-month period.
- 🎨 **Design Choice:** Enhanced readability by shading the area under the line and adding total value labels.
- 📊 **Data Representation:** Plotted monthly defect counts to track changes over time.
- 💡 **Insights Gained:** The data shows a downward trend in total defects, with an approximate 21% decrease over the 6-month period.

#### (2) Repair Cost by Defect Type and Location - Stacked Bar Chart

<img src="/Resources/Images/Bar_Chart.PNG" width="850" height="550" alt="Bar_Chart1.PNG">

- 🛠️ **Excel Features:** Stacked Bar chart that showcases the total repair cost by Defect Type, with each bar segmented by Defect Location costs.
- 🎨 **Design Choice:** Included labels for the total and segmented values on each bar to emphasize cost distribution across Defect Types and Locations.
- 📉 **Data Organization:** Designated Defect Type as the primary variable because it represents a more broader grouping within a classification hierarchy compared to Defect Location.  
- 💡 **Insights Gained:** The most significant groups contributing to repair cost appear to be Functional for Defect Types and Components for Defect Locations.

#### (3) Most Significant Defect - Pivot Table

<img src="/Resources/Images/Product_Table.PNG.PNG" width="850" height="550" alt="Product_Table1.PNG">

- 🛠️ **Excel Features:** Pivot tables listing product ID by their corresponding repair cost total or defect count.
- 🎨 **Design Choice:** Incorporated conditional formatting with data bars to better visualize changes in totals.
- 📉 **Data Organization:** Listed only the top 5 product IDs by highest repair cost total or defect count.
- 💡 **Insights Gained:** Product 81 ranks highest in both cost and frequency; therefore, a root cause analysis is recommended for this product to identify its underlying issues.

#### (4) Repair Cost Breakdown by Severity - Pie Chart

<img src="/Resources/Images/Pie_Chart.PNG" width="850" height="550" alt="Pie_Chart1.PNG">

- 🛠️ **Excel Features:** Pie chart showing the distribution in repair cost among Severity levels.
- 🎨 **Design Choice:** Assigned familiar color coding to each Severity level to enhance clarity (Critical = Red, Moderate = Orange, Minor = Green).
- 📊 **Data Representation:** Shows the percentage contribution of each Severity level by total repair costs.
- 💡 **Insights Gained:** Defect Severity does not appear to differ significantly between each level, which could imply Severity has little impact on cost or the dataset is flawed.

### 🧮 Functions and Formulas

#### (1) Severity with Highest Repair Cost (Pie Chart)

<img src="/Resources/Images/Search2.PNG" width="850" height="550" alt="Search2.PNG">
<img src="/Resources/Images/Search.PNG" width="850" height="550" alt="Search1.PNG">

- Function:
    - =INDEX('Pivot Table'!B19:B21,MATCH(MAX('Pivot Table'!C19:C21),'Pivot Table'!C19:C21,0))

- 🔍 **Index Filtering:** Identifies the row in the pivot table’s 2nd column (sum of repair_cost) with the highest repair cost, then returns the corresponding Severity from the 1st column.
- 🎯 **Pivot Table:** Displays details for each Severity, including contribution to repair cost, defect count, and average repair cost.
- 🔢 **Formula Purpose:** Returns the Severity that contributes most to the total repair cost.

#### (2) Conditional Label Display Formula (Stacked Bar Chart)

<img src="/Resources/Images/Ifs_Statement.gif" width="850" height="550" alt="Ifs_Statement1.PNG">

- Function:
    - =IFS(AND(F13="", F14="", F15=""), "", AND(F14="", F15=""), "",TRUE, F13)
    - =IFS(AND(F13="", F14="", F15=""), "", AND(F14="", F15=""), F13,TRUE, F14)
    - =IFS(AND(F13="", F14="", F15=""), "", AND(F14="", F15=""), "",TRUE, F15)

- 🔍 **IFS Statment:** Adjust the total repair cost above each stacked bar based on which condition is met.
    - **Logical Test 1:** If a 'Defect Location' filter is applied, hide the total repair cost labels.
    - **Logical Test 2:** If a 'Defect Type' filter is applied, only display the total repair cost for the selected Defect Type. 
    - **Logical Test 3:** If neither the 'Defect Location' nor the 'Defect Type' filter is applied, return the total repair cost for each Defect Type.
- 🎯 **Pivot Table:** Provides the total repair cost in a matrix format, broken down by Defect Type and Defect Location.
- 🔢 **Formula Purpose:** Ensures chart labels display correctly by preventing totals from appearing in cases where they are unnecessary (e.g., only one bar is shown or the chart is not stacked).

#### Basic Functions
- =SUM(Defect_Table[repair_cost])

- =COUNTA(Defect_Table[defect_id])

- ="Product"&" "&F3


### 📋 Slicers and Filters ###

<img src="/Resources/Images/Slicer.PNG" width="850" height="550" alt="Slicer1.PNG">

#### Slicer for Defect Categories: Implemented slicers to sort and aggregate data based on four categories: Defect location, Type, Severity, and Inspection Method. 
- Key Benefits:
    - 🗃️ Dynamic Filtering: Users can seamlessly filter the charts to focus on specific defect categories.
    - 👥 Interactivity: Allows users to interact with the dashboard directly to explore and compare different results.

## Conclusion

Designed an interactive dashboard that visualizes monthly defect counts and highlights critical information regarding defect frequency and cost. The dashboard enables users to identify current trends and the most problematic products in order to support data-driven quality improvement decisions.