# Insurance PowerBi Project

## Project Overview

This Power BI report aims to demonstrate my data analysis skills, acquired through my studies, by presenting an end-to-end analysis of a fictional insurance company. The goal is to provide a comprehensive dashboard highlighting key insights such as the total amount of claims by status, category, and age group. Several filters have been added to allow viewers to segment and isolate the data for improved visualization and analysis.

The second page features a table designed to provide a clear overall view of the dataset, incorporating all available filters while maintaining readability from a data interpretation perspective.


### Steps followed 

- Step 1 : Loaded the data into SQL Server Management Studio. The dataset was sourced from a CSV file.
- Step 2 :Loaded the data into Power BI Desktop using SSMS, with the table containing the data set as the data source.
- Step 3 : Opened Power Query Editor and, under the View tab in the Data Preview section, enabled the Column distribution, Column quality, and Column profile.
- Step 4 : By default, column profiling is applied to only 1,000 rows. Changed the setting to Column profiling based on entire dataset.
- Step 5 : Change the data type of the "Age" column to integer.
- Step 6: Changed the data type of the "Claim Date" column to Date.
- Step 7 : Clicked on "Add Column" then "Conditional Column" then used the following formula to create the "Age group" column : If [Age] <= 24 then "Young Adults" else if [Age] <= 60 then "Adults" else "Elders").
- Step 8 :  Changed the data type of the "Age Group" column to Text.
- Step 9 : Clicked on "Add Column" then "Conditional Column" then used the following formula to create the "Active / Inactive" column : If [PolicyEndDate] <= #date(2024, 12, 10) then "Inactive" else "Active").
- Step 10 : Changed the data type of the "Active / Inactive" column to Text.
- Step 11 : Clicked the drop-down arrow in the "Claim Date" column and selected "Remove Empty".
- Step 12 : Renamed the second page from "Sheet" to "Sheet1".
- Step 13 :  Clicked "Use First Row has Headers".
- Step 14 :  Changed the data type of the "Customer Name" column to Text.
- Step 15 : Changed the data type of the "Feedback" column to Text.


### Report creation steps
#### Page 1 - Insurance Data Overview:

- Step 1 : Gender:
A Multi-row card visual was selected using "Gender" and the "Count of Gender".
- Step 2 : Number of Claim by Claim Status:
A Ribbon chart was selected with "ClaimStatus" on the X-axis and "Count of ClaimStatus" on the Y-axis.
- Step 3 : Claim Amount by Age Group:
A Line chart was selected with "Age Group" on the X-axis and "SUM of ClaimAmount" on the Y-axis.
- Step 4 : Premium Amount by Policy Type:
A Stacked bar chart was selected with the "PremiumAmount" on the X-Axis and "PolicyType" on the Y-Axis.
- Step 5 : Count of Active / Inactive Policy:
A Donut chart was selected with the "Active / Inactive" for the Legend and "Count of Active / inactive" for the Values.
- Step 6 : Policy Type:
A Matrix visual was selected with the "PolicyType" for the Rows, "ClaimStatus" for the Columns and the "Sum of CoverageAmount" for the Values .
- Step 7 : Premium Amount:
A card visual was selected displaying the "Premium Amount" for the Data.
- Step 8 : Coverage Amount:
A card visual was selected displaying the "CoverageAmount" for the Data.
- Step 9 : Claim Amount:
A card visual was selected displaying the "ClaimAmount" for the Data.
- Step 10 : Policy Number:
A Slicer with a drop-down menu visual was selected using the "PolicyNumber" for the Field.
- Step 11 : Claim Number:
A Slicer with a drop-down menu visual was selected using the "ClaimNumber" for the Field.
- Step 12 : Customer ID:
A Slicer with a drop-down menu visual was selected using the "CustomerID" for the Field.

<img width="1520" height="836" alt="InsuranceData1" src="https://github.com/user-attachments/assets/52728424-6351-4af1-861c-63845dd71efd" />

#### Page 2 
- General Overview:
           
- Step 1 : Sales by Region:
A Table visual was selected with the following fields used as columns : "PolicyNumber", "CustomerID", "ClaimNumber", "Age", "Gender", "CoverageAmount", "PremiumAmount", "PolicyStartDate", "PolicyEndDate", "PolicyType", "ClaimStatus", "ClaimDate", "ClaimAmount", "Age Group" and "Active/Inactive".
- Step 2 : Left Arrow Navigation:
A left arrow button was added  with a Page Navigator to allow users to easily return to the previous page.

<img width="1518" height="840" alt="InsuranceData2" src="https://github.com/user-attachments/assets/e5cc880c-eaae-4662-a750-cba38843a4a8" />




 # The report was then published to Power BI Service.
 
 ## Report Snapshot (Power BI DESKTOP)


<img width="1869" height="878" alt="InsuranceDatadashboard" src="https://github.com/user-attachments/assets/412dc217-3fca-4203-ab39-1fb3f76aa324" />


# Insights

- The total claim amount decreases significantly across age groups, from Adults with a total of 3.5 million, to Elders at 2.4 million, and Young Adults at 0.7 million..

- The Travel premium policy type represents the highest total claim amount among all policy types, with a total of 1.59 million, while Home represents the lowest, with a total of 0.41 million.

- There is little to no difference in the total number of claims submitted by male and female customers..


