# Enterprise Attrition & Workforce Retention Intelligence Dashboard

## 📊 Project Overview

The Enterprise Attrition & Workforce Retention Intelligence Dashboard is a Power BI business analytics project designed to analyze employee attrition, workforce composition, employee satisfaction, compensation, performance, tenure, and department-level workforce planning.

The project transforms employee and attrition data into an interactive HR analytics solution that helps identify workforce patterns and potential areas requiring management attention.

The dashboard contains three analytical sections:

1. Executive Summary
2. Employee Profile Analysis
3. Operational Root Cause & Manager-Specific Analysis

---

## 🎯 Business Problem

Employee attrition can create significant operational and financial challenges for organizations.

HR and management teams need to understand:

- How many employees are leaving
- Overall attrition rate
- Which departments have more leavers
- Why employees are leaving
- How attrition varies by job level
- Whether satisfaction differs across workforce groups
- How salary and tenure relate to workforce retention
- Which managers have higher numbers of leavers
- How department headcount compares with budget

This project addresses these questions through an interactive Power BI dashboard.

---

## 📌 Key KPIs

The dashboard contains the following major KPIs:

- Total Headcount
- Active Headcount
- Total Leavers
- Attrition Rate
- Average Satisfaction Score
- Average Salary
- Average Tenure
- Voluntary Leavers
- Voluntary Attrition Rate
- Average Salary of Leavers
- Average Satisfaction of Leavers
- Department Headcount Variance

---

## 📈 Dashboard Pages

### 1. Executive Summary

The Executive Summary provides a high-level view of the organization's workforce.

Key visuals include:

- Total Headcount
- Active Headcount
- Total Leavers
- Attrition Rate
- Average Satisfaction Score
- Monthly Leaver Trend
- Leavers by Department
- Attrition by Job Level
- Leavers by Exit Reason

The supplied dashboard snapshot shows:

- Total Headcount: 1,400
- Active Headcount: approximately 1K
- Total Leavers: 223
- Attrition Rate: 15.9%
- Average Satisfaction Score: 3.4218

---

### 2. Employee Profile Analysis

This page analyzes employee characteristics and workforce composition.

Key analyses include:

- Employee performance vs. leavers
- Workforce distribution by tenure
- Workforce distribution by age
- Workforce distribution by salary
- Salary comparison across job levels
- Satisfaction score comparison by department
- Average salary
- Average satisfaction
- Average salary of leavers

---

### 3. Operational Root Cause & Manager-Specific Analysis

This page focuses on operational workforce patterns.

Key visuals include:

- Top managers by attrition rate
- Manager-level leaver analysis
- Department headcount vs. budget
- Destination of leavers
- Exit reasons
- Manager-level employee and leaver analysis

The purpose is to help HR teams investigate workforce retention patterns at a more detailed organizational level.

---

# 🛠️ Tools & Technologies

- Microsoft Power BI
- Power Query
- DAX
- Microsoft Excel
- Data Modeling
- Data Cleaning
- Data Visualization
- Business Intelligence
- HR Analytics

---

# 🧹 Data Preparation

The dataset was prepared for analytical use through Power Query and Power BI.

Key preparation activities included:

- Data type validation
- Employee record preparation
- Attrition event preparation
- Date field preparation
- Workforce categorization
- Tenure band creation
- Salary band creation
- Age group creation
- Date dimension creation
- Relationship creation between tables

---

# 🧮 Data Model

The Power BI model contains multiple analytical tables including:

- employees
- attrition_events
- departments
- Dim_Date

The employee table contains employee-level attributes such as:

- Employee ID
- Full Name
- Department
- Job Level
- Gender
- Tenure
- Salary
- Satisfaction Score
- Performance Rating
- Manager
- Hire Date
- Employment Status
- Last Promotion
- Age

---

# 📊 Key Findings

The dashboard provides visibility into several workforce patterns.

### Workforce Size

The dataset contains 1,400 employee records.

### Attrition

There are 223 recorded leavers.

The overall attrition rate displayed by the dashboard is approximately 15.9%.

### Satisfaction

The dashboard reports an average satisfaction score of approximately 3.42.

### Department Analysis

The dashboard compares employee leavers across departments including:

- Technology
- Operations
- Sales & Distribution
- Risk & Compliance
- Finance
- Unassigned

### Exit Reasons

The dashboard categorizes employee departures into reasons including:

- Voluntary
- Other
- Performance
- Retirement

---

# 📐 DAX Measures

The project uses DAX measures to calculate HR KPIs dynamically.

Important measures include:

### Total Headcount

```DAX
Total Headcount =
COUNTROWS(employees)
Active Headcount
Active Headcount =
CALCULATE(
    COUNTROWS(employees),
    employees[employment_status] = "Active"
)
Total Leavers
Total Leavers =
COUNTROWS(attrition_events)
Attrition Rate
Attrition Rate =
DIVIDE(
    [Total Leavers],
    [Total Headcount],
    0
)
Average Satisfaction Score
Avg Satisfaction Score =
CALCULATE(
    AVERAGE(employees[satisfaction_score]),
    employees[employment_status] = "Active"
)
Average Salary
Avg Salary =
CALCULATE(
    AVERAGE(employees[salary]),
    employees[employment_status] = "Active"
)
Average Tenure
Avg Tenure =
CALCULATE(
    AVERAGE(employees[tenure_years]),
    employees[employment_status] = "Active"
)
Voluntary Leavers
Voluntary Leavers =
CALCULATE(
    COUNTROWS(attrition_events),
    attrition_events[exit_reason] = "Voluntary"
)
Voluntary Attrition Rate
Voluntary Attrition Rate =
DIVIDE(
    [Voluntary Leavers],
    [Total Headcount],
    0
)
Monthly Leavers
Monthly Leavers =
CALCULATE(
    [Total Leavers],
    USERELATIONSHIP(
        attrition_events[exit_date],
        Dim_Date[Date]
    )
)
Average Salary of Leavers
Avg Salary Leavers =
CALCULATE(
    AVERAGE(employees[salary]),
    employees[employment_status] = "Left"
)
Department Headcount Variance
Department Headcount Variance =
[Active Headcount]
-
SUM(departments[headcount_budget])
Average Satisfaction of Leavers
Avg Satisfaction Leavers =
CALCULATE(
    AVERAGE(employees[satisfaction_score]),
    employees[employment_status] = "Left"
)
📊 Calculated Columns
Tenure Band
Tenure Band =
SWITCH(
    TRUE(),
    employees[tenure_years] < 1, "0–1 yr",
    employees[tenure_years] < 3, "1–3 yrs",
    employees[tenure_years] < 5, "3–5 yrs",
    employees[tenure_years] < 10, "5–10 yrs",
    "10+ yrs"
)
Salary Band
Salary Band =
SWITCH(
    TRUE(),
    employees[salary] < 30000, "Under £30K",
    employees[salary] < 50000, "£30K–£50K",
    employees[salary] < 75000, "£50K–£75K",
    employees[salary] <= 100000, "£75K–£100K",
    "Over £100K"
)
Age Group
Age Group =
SWITCH(
    TRUE(),
    ISBLANK(employees[age]), "Unknown",
    employees[age] < 30, "Under 30",
    employees[age] <= 40, "30–40",
    employees[age] <= 50, "40–50",
    "Over 50"
)
🔎 Business Questions Answered

This dashboard can be used to answer questions such as:

What is the organization's current headcount?
How many employees have left?
What is the overall attrition rate?
Which departments have the highest number of leavers?
What are the major exit reasons?
How does attrition vary by job level?
How does employee satisfaction vary across departments?
How does workforce distribution vary by age?
How does workforce distribution vary by tenure?
How does workforce distribution vary by salary?
What is the average salary of active employees?
What is the average salary of employees who left?
How does department headcount compare with budget?
Which managers require further HR investigation based on the dashboard metrics?
How does employee performance relate to leaver counts?
