# Customer Segmentation and Calculated Columns – AdventureWorks

## 1. Assignment Overview

**Table:** Customer Lookup

**Objective:** Enhance customer data by creating calculated columns that classify customers based on parent status, annual income, and education level.

The assignment focuses on implementing business rules using DAX logical functions and conditional expressions.

## 2. Parent

**Column:** Parent

**Purpose:** Identify whether a customer is classified as a parent.

**Values:** Y / N

This field is used as an input for the Customer Priority classification.

**Note:** Document the original source or calculated-column formula here, depending on how this field was obtained.

## 3. Customer Priority

**Column Name:** Customer Priority

**DAX Functions:** IF(), AND()

### Business Question
Which customers should be classified as priority customers based on parent status and annual income?

### Business Rules
- If Parent = "Y" AND Annual Income > 100000, classify as "Priority".
- Otherwise, classify as "Standard".

### DAX Formula (reference)

```dax
Customer Priority =
IF(
    AND(
        'Customer Lookup'[Parent] = "Y",
        'Customer Lookup'[Annual Income] > 100000
    ),
    "Priority",
    "Standard"
)
```

### Explanation
- IF() evaluates the condition and returns the appropriate classification.
- AND() checks whether both conditions are satisfied.
- Customers meeting both conditions receive Priority.
- All other customers receive Standard.

### Business Application
Identify priority customer segments for customer profiling and targeted business analysis.

## 4. Income Level

**Column Name:** Income Level

**DAX Functions:** IF() / nested conditional logic

### Business Question
How can customers be segmented according to their annual income?

### Business Rules
- Annual Income > 150000 → Very High
- Annual Income >= 100000 → High
- Annual Income >= 50000 → Average
- Otherwise → Low

### DAX Formula (reference)

```dax
Income Level =
IF(
    'Customer Lookup'[Annual Income] > 150000,
    "Very High",
    IF(
        'Customer Lookup'[Annual Income] >= 100000,
        "High",
        IF(
            'Customer Lookup'[Annual Income] >= 50000,
            "Average",
            "Low"
        )
    )
)
```

### Explanation
The nested IF() function evaluates income conditions in sequence and assigns an appropriate income category.

### Business Application
Compare customer characteristics and purchasing patterns across income segments.

## 5. Education Category

**Column Name:** Education Category

**DAX Function:** SWITCH()

### Business Question
How can different education levels be grouped into broader educational categories?

### Business Rules
- High School or Partial High School → High School
- Bachelors or Partial College → Undergrad
- Graduate Degree → Graduate

### DAX Formula (reference)

```dax
Education Category =
SWITCH(
    'Customer Lookup'[Education],
    "High School", "High School",
    "Partial High School", "High School",
    "Bachelors", "Undergrad",
    "Partial College", "Undergrad",
    "Graduate Degree", "Graduate",
    BLANK()
)
```

### Explanation
- SWITCH() compares the Education column against specified values.
- Matching education levels are grouped into broader categories.
- BLANK() handles values not covered by the listed rules.

### Business Application
Simplify education-based customer analysis and reporting.

## 6. DAX Concepts Applied

| Function / Concept | Application |
|---|---|
| IF() | Conditional classification |
| AND() | Multiple logical conditions |
| SWITCH() | Category mapping |
| Calculated Columns | Row-level customer classification |
| Nested IF() | Multiple income conditions |

## 7. Expected Outcome

The Customer Lookup table contains customer classification attributes that support:
- Priority customer identification.
- Income-based customer segmentation.
- Education-based customer grouping.
- Customer profiling and business analysis.

## 8. Technologies Used

- Microsoft Power BI Desktop
- Data Analysis Expressions (DAX)
- Customer Lookup table
- Calculated Columns

**Project:** AdventureWorks Sales Analysis  
**Author:** Ravindra Pal  
**Status:** Completed and documented
