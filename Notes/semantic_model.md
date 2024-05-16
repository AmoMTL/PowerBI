# Design a semantic model in Power BI

## Introduction

Creating a great semantic model is one of the most important tasks that a data analyst can perform in Microsoft Power BI. By doing this job well, you help make it easier for people to understand your data, which will make building valuable Power BI reports easier for them and for you.

A good semantic model offers the following benefits:
* Data exploration is faster.
* Aggregations are simpler to build.
* Reports are more accurate.
* Writing reports takes less time.
* Reports are easier to maintain in the future.

Generally, a smaller semantic model is better because it performs faster and will be simpler to use. However, defining what a smaller semantic model entails is equally as problematic because it's a heuristic and subjective concept.

Relationships are defined between tables through primary and foreign keys. Primary keys are column(s) that identify each unique, non-null data row. For instance, if you have a Customers table, you could have an index that identifies each unique customer. The first row has an ID of 1, the second row an ID of 2, and so on. Each row is assigned a unique value, which can be referred to by this simple value: the primary key. This process becomes important when you are referencing rows in a different table, which is what foreign keys do. Relationships between tables are formed when you have primary and foreign keys in common between different tables.

## Star schemas

You can design a star schema to simplify your data. It's not the only way to simplify your data, but it is a popular method; therefore, every Power BI data analyst should understand it. In a star schema, each table within your semantic model is defined as a dimension or a fact table, as shown in the following visual.

![star schema](https://learn.microsoft.com/en-ca/training/modules/design-model-power-bi/media/01-star-schema-example-01-ss.png)

Fact tables contain observational or event data values: sales orders, product counts, prices, transactional dates and times, and quantities. Fact tables can contain several repeated values. 

Dimension tables contain the details about the data in fact tables: products, locations, employees, and order types. These tables are connected to the fact table through key columns. Dimension tables are used to filter and group the data in fact tables.

**Star schemas** and the underlying **semantic model** are the foundation of organized reports; the more time you spend creating these connections and design, the easier it will be to create and maintain reports.

## Create a date table

Suppose that you are developing reports for the Sales team at your organization. The database contains tables for sales, orders, products, and more. You notice that many of these tables, including Sales and Orders, contain their own date columns, as shown by the ShipDate and OrderDate columns in the Sales and Orders tables. You are tasked with developing a table of the total sales and orders by year and month. How can you build a visual with multiple tables, each referencing their own date columns?

To solve this problem, you can create a common date table that can be used by multiple tables. The following section explains how you can accomplish this task in Power BI.

Ways that you can build a common date table are:
* Source data
* DAX
* Power Query

### Source Data

Occasionally, source databases and data warehouses already have their own date tables. If the administrator who designed the database did a thorough job, these tables can be used to perform the following tasks:
* Identify company holidays
* Separate calendar and fiscal year
* Identify weekends versus weekdays

### DAX (Data Analysis Expression)

You can use the Data Analysis Expression (DAX) functions CALENDARAUTO() or CALENDAR() to build your common date table. The CALENDAR() function returns a contiguous range of dates based on a start and end date that are entered as arguments in the function. Alternatively, the CALENDARAUTO() function returns a contiguous, complete range of dates that are automatically determined from your semantic model. The starting date is chosen as the earliest date that exists in your semantic model, and the ending date is the latest date that exists in your semantic model plus data that has been populated to the fiscal month that you can choose to include as an argument in the CALENDARAUTO() function. 


In Power BI Desktop, select New Table, and then enter in the following DAX formula:
```
Dates = CALENDER(DATE(2011, 5, 31), DATE(2022,12, 31))
```

Now, you have a column of dates that you can use. However, this column is slightly sparse. You also want to see columns for just the year, the month number, the week of the year, and the day of the week. You can accomplish this task by selecting New Column on the ribbon and entering the following DAX equation, which will retrieve the year from your Date table.

```
Year = YEAR(Dates[Date])
```
You can perform the same process to retrieve the month number, week number, and day of the week:
```
MonthNum = MONTH(Dates[Date])
```

```
WeekNum = WEEKNUM(Dates[Date])
```

```
Days of the week = FORMAT(Dates[Date], "DDDD")
```
When you have finished, your table will contain the columns that are shown in the following figure.
![DAX ex 1](https://learn.microsoft.com/en-ca/training/modules/design-model-power-bi/media/03-final-columns-dax-table-2-ss.png)

### Power Query

You can use M-language, the development language that is used to build queries in Power Query, to define a common date table.

Select Transform Data in Power BI Desktop, which will direct you to Power Query. In the blank space of the left Queries pane, right-click to open the following drop-down menu, where you will select New Query > Blank Query.

In the resulting New Query view, enter the following M-formula to build a calendar table:

```
= List.Dates(#date(2011,05,31), 365*10, #duration(1,0,0,0))
```

![power query to build date table](https://learn.microsoft.com/en-ca/training/modules/design-model-power-bi/media/03-m-query-common-data-table-04-ss.png)

For your sales data, you want the start date to reflect the earliest date that you have in your data: May 31, 2011. Additionally, you want to see dates for the next 10 years, including dates in the future. This approach ensures that, as new sales data flows in, you won't have to re-create this table. You can also change duration. In this case, you want a data point for every day, but you can also increment by hours, minutes, and seconds.

### Mark as the official date table

Your first task in marking your table as the official date table is to find the new table on the Fields pane. Right-click the name of the table and then select Mark as date table, as shown in the following figure.

## Build visual

To build your visual between the Sales and Orders tables, you will need to establish a relationship between this new common date table and the Sales and Orders tables. As a result, you will be able to build visuals by using the new date table. To complete this task, go to Model tab > Manage Relationships, where you can create relationships between the common date table and the Orders and Sales tables by using the OrderDate column. The following screenshot shows an example of one such relationship.

![buildmodel](https://learn.microsoft.com/en-ca/training/modules/design-model-power-bi/media/03-create-relationship-8-ss.png)

To determine the total sales, you need to add all sales because the Amount column in the Sales table only looks at the revenue for each sale, not the total sales revenue. You can complete this task by using the following measure calculation, which will be explained in later discussions. The calculation that you will use when building this measure is as follows:

```
#Total Sales = SUM(Sales[‘Amount’])
```

After you have finished, you can create a table by returning to the Visualizations tab and selecting the Table visual. You want to see the total orders and sales by year and month, so you only want to include the Year and Month columns from your date table, the OrderQty column, and the #TotalSales measure. When you learn about hierarchies, you can also build a hierarchy that will allow you drill down from years to months. For this example, you can view them side-by-side. You have now successfully created a visual with a common date table.

![build model 2](https://learn.microsoft.com/en-ca/training/modules/design-model-power-bi/media/03-common-date-dax-5-ss.png)

## Work with dimensions

You can use hierarchies as one source to help you find detail in dimension tables. These hierarchies form through natural segments in your data. For instance, you can have a hierarchy of dates in which your dates can be segmented into years, months, weeks, and days. Hierarchies are useful because they allow you to drill down into the specifics of your data instead of only seeing the data at a high level.

In the preceding Date column, the date is shown in increasingly finer detail through year, quarters, months, and days. You can also manually create hierarchies.

For example, consider a situation where you want to create a stacked bar chart of Total Sales by Category and Subcategory. You can accomplish this task by creating a hierarchy in the Product table for categories and subcategories. To create a hierarchy, go to the Fields pane on Power BI and then right-click the column that you want the hierarchy for. 

