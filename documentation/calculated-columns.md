# Calculated Columns and Product Classification – AdventureWorks

## 1. Overview

This document records additional DAX calculated-column assignments completed in the AdventureWorks Power BI project.

The objective is to enhance the existing Calendar Lookup, Customer Lookup, and Product Lookup tables with useful date attributes, customer information, and product classifications.

## 2. Month Abbreviation Formatting

**Table:** Calendar Lookup

**Column:** MonthShortName

### Assignment Question
How can month abbreviations be displayed in uppercase to improve readability in reports?

### Requirement
Update the MonthShortName column to capitalize the first three characters of the month name.

### DAX Formula (reference)

```dax
MonthShortName =
UPPER(
    LEFT(
        'Calendar Lookup'[Month Name],
        3
    )
)
```

### Explanation
- LEFT() extracts the first three characters.
- UPPER() converts the extracted characters into uppercase.

### Example

| Month Name | MonthShortName |
|---|---|
| January | JAN |
| February | FEB |
| March | MAR |
| April | APR |
| December | DEC |

### Business Application
Improves consistency and readability of month labels in charts, slicers, and reports.

## 3. SKU Category Extraction

**Table:** Product Lookup

**Column:** SKU Category

### Assignment Question
How can the category portion of a product SKU be extracted?

### Requirement
Create a calculated column named SKU Category that extracts the characters appearing before the hyphen in the Product SKU column.

### DAX Formula (reference)

```dax
SKU Category =
LEFT(
    'Product Lookup'[Product SKU],
    SEARCH(
        "-",
        'Product Lookup'[Product SKU]
    ) - 1
)
```

### Explanation
- SEARCH() locates the hyphen in the SKU.
- Subtracting 1 identifies the number of characters before the hyphen.
- LEFT() extracts those characters.

### Business Application
Enables product classification using SKU prefixes and supports product-level analysis.

### Separate SKU Category Table

The distinct SKU categories can be stored in a separate calculated table.

```dax
DimSKUCategory =
DISTINCT(
    SELECTCOLUMNS(
        'Product Lookup',
        "SKU Category",
        'Product Lookup'[SKU Category]
    )
)
```

**Purpose:** Maintain a separate list of unique SKU categories for product classification and reporting.

## 4. Birth Year Extraction

**Table:** Customer Lookup

**Column:** BirthYear

### Assignment Question
How can only the year be extracted from the BirthDate field?

### Requirement
Create a new column named BirthYear in Customer Lookup.

### DAX Formula (reference)

```dax
BirthYear =
YEAR(
    'Customer Lookup'[BirthDate]
)
```

### Explanation
- YEAR() extracts the year component from a date.
- The resulting column stores the customer's birth year.

### Example

| BirthDate | BirthYear |
|---|---:|
| 15/04/1985 | 1985 |
| 22/08/1990 | 1990 |
| 10/12/2000 | 2000 |

### Business Application
Supports customer demographic analysis and age-group segmentation.

## 5. Date Difference Calculation

**Table:** Calendar Lookup

**Column:** DateDiff

### Assignment Question
How can the difference between two dates be calculated?

### DAX Function
DATEDIFF()

### General DAX Syntax

```dax
DATEDIFF(
    <StartDate>,
    <EndDate>,
    <Interval>
)
```

### Explanation
- StartDate specifies the beginning date.
- EndDate specifies the ending date.
- Interval specifies the unit of calculation, such as DAY, MONTH, or YEAR.

### Possible Applications
- Calculate the number of days between two dates.
- Analyze elapsed time.
- Support date-based reporting and comparisons.

**Note:** Insert the exact DATEDIFF formula used in your Power BI file here. The screenshots show the DateDiff column, but do not establish its exact start date, end date, or interval.

## 6. Product Subcategory Classification

**Table:** Product Lookup / Product Subcategories Lookup

### Objective
Organize products according to their associated product subcategories.

### Analytical Purpose
- Group products into meaningful subcategories.
- Support product-level reporting.
- Enable category and subcategory comparisons.

**Note:** Add the exact calculated column or relationship details here according to the implementation in your PBIX file.

## 7. DAX Functions and Concepts Practised

| Function | Purpose |
|---|---|
| UPPER() | Convert text into uppercase |
| LEFT() | Extract characters from the beginning of text |
| SEARCH() | Find the position of a character or text |
| YEAR() | Extract the year from a date |
| DATEDIFF() | Calculate the difference between two dates |
| DISTINCT() | Return unique values |
| SELECTCOLUMNS() | Create a table with selected columns |

## 8. Skills Demonstrated

- DAX calculated columns
- Date and time functions
- Text manipulation
- Product classification
- Customer demographic analysis
- Distinct value extraction
- Calculated tables
- Data modeling

## 9. Project Status

The above assignments have been implemented as part of the ongoing AdventureWorks Power BI project.

**Tool:** Microsoft Power BI Desktop  
**Language:** Data Analysis Expressions (DAX)  
**Author:** Ravindra Pal  
**Project:** AdventureWorks Sales Analysis
