# Housing analysing PowerBi Project

## Project Overview

This Power BI report provides an end-to-end analysis of the current housing market in Denmark. The goal is to understand the market’s evolution and conditions by analyzing trends and patterns, thereby identifying the factors that influence its trajectory. The project uses metrics designed for individuals interested in investing in this market, taking into account regional differences, inflation rates, and purchase prices.


### Steps followed 

- Step 1 : Loaded the data into Google BigQuery. The dataset is a csv file.
- Step 2 : Loaded the data into Power BI Desktop, using Google BigQuery has the datasource.
- Step 3 : Opened Power Query Editor and, under the View tab in the Data Preview section, enabled the Column distribution, Column quality, and Column profile options.
- Step 4 : By default, column profiling is applied to only 1,000 rows. Changed the setting to Column profiling based on entire dataset.
- Step 5 : Change the data type of the column name "%_change_between_offer_and_purchase" to Percentage.
- Step 6 : Replace null values in the "City" column with "Unknown".
- Step 7 : Replace null values in the "dk_ann_infl_rate%" column with 1.85 to closely match the existing data.
- Step 8 : Replace null values in the "yield_on_mortgage_credit_bonds%" column with 1.47 to closely match the existing data.
- Step 9 : Created the Measure Table 1, then defined the following measures using DAX: "Last 12 Months Sales", "Median Sales Price Changes", "Unit Sold in Latest Year and Quarter" and "YOY (Year on Year) Sales Growth".
- Step 10 : Created the Measure Table 2, then defined the following measures using DAX: "Average Price SQM", "Offer to SQM Ratio", "Sales by Region" and "Total YTD Sales".
- Step 11 : Created the Offer Price column in the Housing1 table using DAX.
- Step 12 : Create the Age column in the Housing1 table using DAX.

### DAX Query used: 
- 1: Last 12 Months Sales = CALCULATE(SUM(Housing1[purchase_price]),DATESINPERIOD(Housing1[date],MAX(Housing1[date]), -12,MONTH))
- 2: Median Sales Price Changes = 
VAR CurrentMediantPrice =
    MEDIANX(FILTER(Housing1,
    YEAR(Housing1[date].[Date])=
    YEAR(MAX(Housing1[date]))),
    Housing1[purchase_price])
VAR PreMedianPrice = 
    MEDIANX(FILTER(Housing1,YEAR(Housing1[date].[Date]) = YEAR(MAX(Housing1[date].[Date])) -1), Housing1[purchase_price])

RETURN
    IF(PreMedianPrice<>0,(CurrentMediantPrice-PreMedianPrice)/PreMedianPrice,
    BLANK())
- 3:Unit Sold in Latest Year and Quarter = 
CALCULATE(DISTINCTCOUNT(Housing1[house_id]),YEAR(Housing1[date])=Year(MAX(Housing1[date])) && QUARTER(Housing1[date])=QUARTER(MAX(Housing1[date])))
- 4:YOY Sales Growth = 
    Var CurrYearSales = 
        CALCULATE(SUM(Housing1[purchase_price]),
              Year(Housing1[date]) = YEAR(MAX(Housing1[date])))
Var Previyearsales = 
    CALCULATE(SUM(Housing1[purchase_price]),
    YEAR(Housing1[date])=YEAR(MAX(Housing1[date])) -1)

RETURN  
    IF(Previyearsales<>0, (CurrYearSales-Previyearsales) / Previyearsales, blank())
- 5: Average Price SQM = AVERAGE(Housing1[sqm_price])
- 6: Offer to SQM Ratio = DIVIDE(SUM(Housing1[Offer Price]), SUM(Housing1[sqm]))
- 7: Sales by Region = 
CALCULATE(SUM(Housing1[purchase_price]),ALLEXCEPT(Housing1,Housing1[region]))
- 8: Total YTD Sales = TOTALYTD(SUM(Housing1[purchase_price]),Housing1[date].[Date]) 
- 9: Offer Price = (100* Housing1[purchase_price]) /(100- Housing1[%_change_between_offer_and_purchase])
- 10: Age = ABS(YEAR(Housing1[date].[Date]) - Housing1[year_build])

### Report creation steps
#### Page 1 - House Market Overview:

- Step 1 : Median Sales Price Changes by region:
A stacked bar chart was selected with "region" on the Y-axis and "Median Sales Price Changes" on the X-axis.
- Step 2 : YOY Sales Growth by Sales type:
A line chart was selected with "sales_type" on the X-axis and "YOY Sales Growth" on the Y-axis.
- Step 3 : Unit Sold and Last 12 Months Sales:
Two card visuals were added to the canvas: one displaying the total amount of unit sold in the latest year and quarter, and the other one showing the total amount of monthly sales in the last 12 months.
- Step 4 : Offer Price vs Purchase Price:
A Scatter chart was selected with the "Offer Price" for the X-Axis and the "purchase_price" on the Y-Axis.


<img width="1167" height="642" alt="Housing analysing report page 1" src="https://github.com/user-attachments/assets/fef9c00d-1ca3-4600-a470-040270b57f65" />



#### Page 2 - Sales and Performances:
           
- Step 1 : Sales by Region:
A stacked bar chart was selected with "region" on the Y-axis and "Sales by Region" on the X-axis.
- Step 2 : Offer to SQM Ratio by Sales Type:
A stacked bar chart was selected with "sales_type" on the Y-axis and "Offer to SQM Ration" on the X-axis.
- Step 3 : Average Price per SQM by Region:
A Donut chart was selected with "region" on the Y-axis and "Average Price SQM" on the X-axis.
- Step 4 : Key influencers:
A Key influencers chart was used with the "purchase_price" set as the Analyze field and the "Age" as the Explain by field.
- Step 5 : A table visual was selected displaying the "date", "Total YTD Sales" and "Sum of purchase_price" 


<img width="1131" height="648" alt="Housing analysing report page 2" src="https://github.com/user-attachments/assets/15443aa9-ccb2-40c9-9741-ec3521825d40" />

 #### Page 3 - House Type:

- Step 1 : Average of Offer Price and Purchase Price by House Type:
A clustered bar chart was selected with "house_type" on the Y-axis and "Average of Offer Price" and "Average of purchase_price" on the X-axis.
- Step 2 : Average Annual Inflation Rate, Interest Rate and Yield on Mortage by House Type:
A clustered bar chart was selected with "house_type" on the Y-axis and "Inflation","Interest" and "Yield" on the X-axis.
- Step 3 : Average SQM and SQM Price by House Type:
A line and stack column chart was selected with "house_type" on the X-axis and "SQM" on column y-axis and SQM Price on the line y-axis.
- Step 4 :Two slicers were selected to the canvas and applied at the page level: one for "City" and the other one for "Area" both using a drop down menu.

<img width="1163" height="650" alt="Housing analysing report page 3" src="https://github.com/user-attachments/assets/2e49b7ee-1686-4c06-8a57-ae17af259103" />


 # The report was then published to Power BI Service.
 
 ## Report Snapshot (Power BI DESKTOP)


<img width="1869" height="920" alt="Housing analysing published 1" src="https://github.com/user-attachments/assets/a0a5fce1-1838-47a5-8362-53606c15b772" />

# Insights

- Farms have the highest average offer and purchase price per square meter, as well as the highest annual inflation rate, interest rate, and mortgage yield among all property types.

- Zealand records the highest total number of sales among the four regions, while Jutland shows the strongest sales price growth throughout the year.

- The regular sales type receives the highest average offer per square meter, whereas the auction sales type consistently receives the lowest offer per square meter over the years.


