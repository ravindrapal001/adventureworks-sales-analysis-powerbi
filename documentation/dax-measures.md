## File Updated
`AdventureWork2.pbix`

## Assignment: Creating DAX Measures in Power BI

### Objective
Create a dedicated Measures table and develop reusable DAX measures to calculate important business metrics for AdventureWorks sales analysis.

### Measures Created

#### 1. SumOfOrderQuantity
**DAX Function:** SUM()

**Formula:**
```dax
SumOfOrderQuantity =
SUM('sales data'[OrderQuantity])
```
**Business Question:** What is the total quantity of products ordered?

**Purpose:** Calculate the total number of units ordered across sales transactions.

#### 2. SumOfReturnQuantity
**DAX Function:** SUM()

**Formula:**
```dax
SumOfReturnQuantity =
SUM('Returns Data'[ReturnQuantity])
```
**Business Question:** What is the total quantity of products returned?

**Purpose:** Measure the overall volume of returned products.

#### 3. TotalCustomers
**DAX Function:** DISTINCTCOUNT()

**Formula:**
```dax
TotalCustomers =
DISTINCTCOUNT('sales data'[CustomerKey])
```
**Business Question:** How many unique customers have placed orders?

**Purpose:** Count distinct customers based on their customer keys rather than counting individual sales transactions.

#### 4. Bulk Orders
**Formula:**
```dax
Bulk Orders =
CALCULATE([TotalOrders],'sales data'[OrderQuantity]>1)
```
**Business Question:** Calculate a Bulk Orders measure that captures the order greater than
1.

#### 5. Total Bikes Sold
```dax
TotalBikeSold =
CALCULATE([TotalOrders],'Categories Lookup'[CategoryName]="Bikes")
```
**Business Question:** How many bike have sold?

#### 6. Total Bikes Return
```dax
TotalBikeReturn =
CALCULATE([SumOfReturnQuantity],'Categories Lookup'[CategoryName]="Bikes")
```
***Business Question:** How many bike has return after sold?

#### 7. Bike Return Rate
```dax
BikeReturnRate =
CALCULATE([Return Rate],'Categories Lookup'[CategoryName]="Bikes")*100
```
** Business Problem:** What is the Bike return Rate?


### Concepts Applied
- DAX Measures
- SUM()
- DISTINCTCOUNT()
- Dedicated Measures Table
- Business KPI Calculation
- Sales and Customer Analysis

### Analytical Applications
These measures provide a foundation for analyzing order quantities, product returns, and customer activity. They can be used in Power BI cards, charts, KPI visuals, and interactive dashboards.

**Project:** AdventureWorks Sales Analysis | Power BI
**Status:** In Progress
