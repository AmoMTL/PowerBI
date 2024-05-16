# Clean, transform and load data into Power BI

## Merging and appending queries

**Merging Queries**: adding columns
**Appending queries**: adding rows

## Pivot/unpivot tables

## Remove rows/columns

## Rename queries

## Replace missing/null values/Remove duplicates

## Change column data type

## Profile data in Power BI

## Use advanced editor to modify M code

Each Power Query step will roughly align with one or two lines of M code. You don't have to be an expert in M code to be able to read it. You can even experiment with changing it. For instance, if you need to change the name of a database, you could do it right in the code and then select Done.

You might notice that M code is written top-down. Later steps in the process can refer to previous steps by the variable name to the left of the equal sign. Be careful about reordering these steps because it could ruin the statement dependencies. Write to a query formula step by using the in statement. Generally, the last query step is used as the in final data set result.