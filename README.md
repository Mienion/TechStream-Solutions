# TechStream-Solutions
# Introduction 
## Context
You have been hired for a new job as a Data Analyst.

The company is called "TechStream Solutions", and the product is a Software as a Service (SaaS) platform named "Streamline Pro". This platform provides comprehensive project management and collaboration tools for businesses of all sizes.

TechStream Solutions has been operating for several years and has gathered significant data on their costs and revenues. They are now looking to analyze their unit economics to understand the profitability of Streamline Pro on a per-customer basis.

The datasets are in the shared folder on Google Drive:
https://drive.google.com/drive/folders/1qhOW9Y2orRXuzbX-kXEmuJ7TMQiRs2Uv?usp=drive_link

By performing these calculations, TechStream Solutions aims to:

* Identify the profitability of acquiring and retaining customers.
* Assess the efficiency of their marketing and sales strategies.
* Make informed decisions on scaling their operations and optimizing their resource allocation.
* This information will guide TechStream Solutions in refining their business strategies, ensuring sustainable growth, and maximizing profitability.

# What should I do?
Today you need to calculate Unit Economics for "TechStream Solutions" including:

* CAC
* ARPU
* COGS
* Gross Margin
* LTV
* LTV / CAC

For doing this you need to use Python + Pandas + Google Colab.

The calculations should be made based on the data from the shared Google Drive folder (the link is in the block above).

# You received the 1st work email with a new job
**Date:** 10 Apr 2023

**From:** Camryn Carroll (camryn@techstream.com)

**Subject:** Welcome to TechStream Solutions: Your First Data Analysis Task!

Dear New Analyst,

Welcome to TechStream Solutions! We are thrilled to have you join our team as a Data Analyst. Your skills and expertise will be invaluable to us as we continue to grow and innovate with our flagship product, Streamline Pro.

At TechStream Solutions, we pride ourselves on our collaborative and data-driven culture. We believe that insightful data analysis is key to making informed decisions and driving our success. As part of your onboarding process, we have an exciting first task that will not only help you get acquainted with our data but also demonstrate the impact of your analysis on our strategic decisions.

**Your First Task: Calculating Unit Economics for Streamline Pro**
**Background:** Streamline Pro is a comprehensive project management and collaboration tool designed to help businesses manage projects, track progress, and collaborate efficiently. Understanding the unit economics of Streamline Pro is crucial for evaluating its financial health and sustainability. This involves analysing key metrics such as Customer Acquisition Cost (CAC), Average Revenue Per User (ARPU), Cost of Goods Sold (COGS), Gross Margin, Customer Lifetime Value (LTV), and the LTV/CAC ratio.

**Objective:** Your task is to calculate the unit economics for Streamline Pro for the month of March 2023. This will help us assess the profitability and efficiency of our customer acquisition strategies and operational expenses.

**Let's start it!**

# 1. Customer Acquisition Cost (CAC)

First, let's import the needed libraries: Pandas
```# PUT YOUR CODE HERE 
import pandas as pd
```
With CAC Formula 

**CAC = Total Marketing & Sales Expenses / Number of New Customers Acquired**

We need to calculate the following figures:

## 1.1 Monthly spending for saleforces
The code is
```
monthly_expenses = pd.read_excel('https://docs.google.com/spreadsheets/d/10OGbaywwMIqKgnPGy8VDvpBVtjyqln47iYa2lFhI9Mw/export?format=xlsx') # extract data

monthly_expenses_lastmonth = monthly_expenses[monthly_expenses['month'] == '2023-03-01'] # lọc chi phí của tháng 3

monthly_expenses_lastmonth_saleforces = monthly_expenses_lastmonth[monthly_expenses_lastmonth['item'] == 'Salesforce'] # lọc từ bảng chi phí của tháng 3 nhưng chi phí liên quan tới bán hàng

monthly_spending = monthly_expenses_lastmonth_saleforces['amount'].sum() # cộng tổng cộng amount trong bảng chi phí bán hàng tháng 3

Print(monthly_spending) # in kết quả
```

## 1.2 Salary for sales and marketing

The code is
```
payroll = pd.read_excel('https://docs.google.com/spreadsheets/d/1c_WihqTZCQvNgxzmd-OwhR9i5diwtfxXVLyMn8R-Lp4/export?format=xlsx') # extract data
payroll_lastmonth = payroll[payroll['month'] == '2023-03-01'] # lọc chi phí của tháng 3
payroll_lastmonth_sale_marketing = payroll_lastmonth[payroll_lastmonth['department'].isin(['Sale','Marketing'])] # lọc từ bảng chi phí của tháng 3 nhưng chi phí liên quan tới bán hàng và marketing
payroll_spending = payroll_lastmonth_sale_marketing['paid'].sum() # cộng tổng cộng lương trả cho marketing và sale tháng 3
Print(payroll_spending) # in kết quả
```
## 1.3 Marketing cost

The code is
```
daily_marketing_spending = pd.read_excel('https://docs.google.com/spreadsheets/d/1AZOIThOV4P-0eYDge53ZwumVkfkHoYPWxst3k3Bv87c/export?format=xlsx') # extract data
daily_marketing_cost = daily_marketing_spending[(daily_marketing_spending['date'].dt.month == 3) & (daily_marketing_spending['date'].dt.year = 2023)] # lọc dòng của tháng 3
marketing_spending = daily_marketing_cost['spending'].sum() # cộng tổng chi phí marketing tháng 3
Print(marketing_spending) # in kết quả
```

## 1.4 Number of new customers
The code is
```
receipts_history = pd.read_excel('https://docs.google.com/spreadsheets/d/1qayqML1zCKdmtzutkcy9LWvE6xFRm6TGBEVkHHJKIuE/export?format=xlsx') # extract data
receipts_history_lastmonth = receipts_history[(receipts_history['date'].dt.month == 3) & (receipts_history['date'].dt.year = 2023)] # lọc dòng của tháng 3
new_customer_lastmonth = receipts_history_lastmonth['new_customer'].sum() # cộng tổng cột new_customer
Print(new_customer_lastmonth) # in kết quả
```
####   Here, we have
**CAC is:**
``` 
CAC = (monthly_spending + payroll_spending + marketing_spending)/new_customer_lastmonth
Print(CAC)
```
**The result is: 1156.83**

## 2. Average Revenue Per User (ARPU)

With ARPU Formula

ARPU = Total Revenue / Number of Users

We need to calculate the following figures:

2.1 Total Revenue
```
total_revenue = receipts_history[(receipts_history['date'].dt.month == 3) & (receipts_history['date'].dt.year == 2023)]['receipt_amount'].sum()
print(total_revenue)
```
2.2 Number of customers
```
number_customner = receipts_history[(receipts_history['date'].dt.month == 3) & (receipts_history['date'].dt.year == 2023)]['customer_id'].count()
print(number_customner)
```
Here, we have
ARPU is:
```
ARPU = total_revenue/number_customner
print(ARPU)
```
**The result is: 266.98**

## 3. COGS
With COGS Formula
**COGS = Beginning Inventory + Purchases During the Period − Ending Inventory**

In the case of a technology company with no physical inventory, COGS is typically calculated based on direct labor costs — such as product team salaries — combined with allocated operational expenses that directly support product development, including server and software expenses

We need to calculate the following figures:

3.1 Server and software costs

```
server_lastmonth = monthly_expenses_lastmonth[monthly_expenses_lastmonth['item'].isin(['AWS Hosting','Google Cloud Storage','Atlassian Jira'])]['amount'].sum()
print(server_lastmonth)
```

```
software_lastmonth = monthly_expenses_lastmonth[monthly_expenses_lastmonth['item'].isin(['Slack','Zoom'])]['amount'].sum()
print(software_lastmonth)
```

3.2 Salary for product team
```
product_team_salary = payroll_lastmonth[payroll_lastmonth['department'] == 'Engineering']['paid'].sum()
print(product_team_salary)
```
**Here, we have COGS is:**
```
COGS = product_team_salary + server_lastmonth + software_lastmonth
print(COGS)
```
**The result is: 20840**

## 4. Gross Margin
With Gross Margin Formula 

**Gross Margin = (Total Revenue - COGS)/Total Revenue*100**

Here we have 
**Gross Margin is:**
```
gross_margin = (total_revenue - COGS)/total_revenue*100
print(gross_margin)
```
**The result is: 74.90**

## 5. Customer lifetime Value
With Customer lifetime Value Formula 

**Customer lifetime Value = ARPU x average customer_lifespan x gross_margin**

We need to calculate the following figure customer_lifespan

First, we need to delect all rows having churn_date is null
```
customer_lifespan_data = customer_lifespan_data.dropna(subset=['churn_date'])
```
Then average customer_lifespan will be
```
customer_lifespan_days = (customer_lifespan_data['churn_date'] - customer_lifespan_data['start_date']).dt.days
avg_customer_lifespan = customer_lifespan_days.mean()/30
print(avg_customer_lifespan)
```
**Here, we have Customer lifetime Value is:**
```
ltv = ARPU*avg_customer_lifespan*gross_margin/100
print(ltv)
```
**The result is: 1968**

## 6. LTV / CAC
we have LTV/CAC is
```
ltv_CAC = ltv/CAC_lastmonth
print(ltv_CAC)
``` 
**The result is: 1.7**
