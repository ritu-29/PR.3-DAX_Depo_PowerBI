# 📊 DAX Depo – Advanced DAX Calculations in Power BI
VIDEO LINK: https://drive.google.com/file/d/1Jelkc1xB9CjNhdqHgklYgBxADlAhl9gT/view?usp=sharing
## 📌 Project Overview
The **DAX Depo** project focuses on building a robust backend data model and performing advanced analytical calculations using **DAX (Data Analysis Expressions)** in Power BI.

The goal is to evaluate how effectively business metrics, KPIs, and time-based insights can be generated using DAX **without relying on multiple visuals**, using only a **Matrix visual** for output.

---

## 🎯 Objectives
- Build a structured data model using fact and dimension tables
- Perform advanced calculations using DAX
- Apply filter context and time intelligence
- Generate business insights using only Matrix visual

---

## 🗂️ Dataset Tables
The project uses the following tables:

- **Sales_Fact** – Contains sales transactions  
- **Returns_Fact** – Contains return data  
- **Customer_Dim** – Customer details  
- **Product_Dim** – Product information  
- **Date_Dim** – Date table for time analysis  
- **Region_Dim** – Regional data  

---

## 🔗 Data Model
A **star schema** is implemented:

- Fact Tables: Sales_Fact, Returns_Fact  
- Dimension Tables: Customer, Product, Date, Region  
- Relationships are properly defined for accurate calculations  

---

## 🧮 Calculated Columns

### 1. Profit
```DAX
Profit = Sales_Fact[SalesAmount] - Sales_Fact[Cost]
````

### 2. Return Flag

```DAX
ReturnFlag =
IF(
    Sales_Fact[SalesID] IN VALUES(Returns_Fact[SalesID]),
    "Returned",
    "Not Returned"
)
```

### 3. Customer Full Name

```DAX
Full Name =
Customer_Dim[FirstName] & " " & Customer_Dim[LastName]
```

---

## 📏 Measures

### Total Sales

```DAX
Total Sales = SUM(Sales_Fact[SalesAmount])
```

### Total Cost

```DAX
Total Cost = SUM(Sales_Fact[Cost])
```

### Total Profit

```DAX
Total Profit = [Total Sales] - [Total Cost]
```

### Return Rate

```DAX
Return Rate =
DIVIDE(
    COUNTROWS(Returns_Fact),
    COUNTROWS(Sales_Fact),
    0
)
```

### Average Sale

```DAX
Avg Sale = AVERAGE(Sales_Fact[SalesAmount])
```

---

## ⚡ Quick Measures

### Year-over-Year Growth

```DAX
YoY Growth =
DIVIDE(
    [Total Sales] - CALCULATE([Total Sales], SAMEPERIODLASTYEAR(Date_Dim[Date])),
    CALCULATE([Total Sales], SAMEPERIODLASTYEAR(Date_Dim[Date]))
)
```

### Month-over-Month Difference

```DAX
MoM Difference =
[Total Sales] - CALCULATE(
    [Total Sales],
    DATEADD(Date_Dim[Date], -1, MONTH)
)
```

---

## 🔄 Filter Context Functions

### Sales (Ignoring Filters)

```DAX
Sales All Regions =
CALCULATE([Total Sales], ALL(Region_Dim))
```

### Conditional Sales

```DAX
High Sales =
CALCULATE(
    [Total Sales],
    FILTER(Sales_Fact, Sales_Fact[SalesAmount] > 1000)
)
```

---

## 🔗 Relationship Functions

### RELATED

```DAX
Region Name = RELATED(Region_Dim[Region])
```

### RELATEDTABLE

```DAX
Total Sales per Customer =
SUMX(
    RELATEDTABLE(Sales_Fact),
    Sales_Fact[SalesAmount]
)
```

---

## 🕒 Time Intelligence

### Year-to-Date (YTD)

```DAX
YTD Sales =
TOTALYTD([Total Sales], Date_Dim[Date])
```

### Last Year Sales

```DAX
Last Year Sales =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(Date_Dim[Date])
)
```

### Running Total

```DAX
Running Total =
CALCULATE(
    [Total Sales],
    DATESBETWEEN(
        Date_Dim[Date],
        MIN(Date_Dim[Date]),
        MAX(Date_Dim[Date])
    )
)
```

---

## 🔁 Iterator Functions

### SUMX

```DAX
Total Profit X =
SUMX(
    Sales_Fact,
    Sales_Fact[SalesAmount] - Sales_Fact[Cost]
)
```

### AVERAGEX

```DAX
Avg Profit =
AVERAGEX(
    Sales_Fact,
    Sales_Fact[SalesAmount] - Sales_Fact[Cost]
)
```

---

## 🔀 Conditional Logic

### SWITCH Example

```DAX
Sales Category =
SWITCH(
    TRUE(),
    Sales_Fact[SalesAmount] < 500, "Low",
    Sales_Fact[SalesAmount] < 2000, "Medium",
    "High"
)
```

---

## 📊 Final Output

A **Matrix Visual** is used to display results:

### Rows:

* Region
* Product Category
* Customer Segment

### Columns:

* Month

### Values:

* Total Sales
* Total Profit
* Return Rate
* YTD Sales
* Running Total

---

## ⚠️ Project Constraints

* Only **Matrix visual** is used
* No charts or additional visuals
* Focus is purely on DAX calculations

---

## 🚀 Key Learnings

* Advanced DAX calculations
* Filter context manipulation
* Time intelligence functions
* Data modeling (Star Schema)
* Performance optimization techniques

---

## 💡 Conclusion

This project demonstrates how powerful DAX can be in generating insights without heavy reliance on visuals. It highlights the importance of data modeling, calculation logic, and business understanding in Power BI.

---

## 📎 Dataset Link

https://docs.google.com/spreadsheets/d/1pwutXoau5k-P6upYP_wOR_CCVEl3YfslcEPmHP-f2sM/edit

---



