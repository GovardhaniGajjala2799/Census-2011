
# India Population Census 2011 Analysis

INTRODUCTION:

The 2011 Census of India is a comprehensive dataset that provides a wealth of information on the demographic, social, and economic characteristics of the country. As a decennial exercise, the Census serves as a crucial benchmark for measuring India's progress and development across various indicators. This project aims to leverage the insights gleaned from the 2011 Census data to generate actionable intelligence that can inform policymaking, resource allocation, and strategic planning at the national and subnational levels.

## Data Exploration and Cleaning

The dataset includes information on various metrics such as population, literacy rate, sex ratio, growth rate, and geographical area at the state and district levels. The data was first inspected for any missing values or inconsistencies, and necessary cleaning was performed to ensure data integrity.
## Tools Used 🛠️

Database: MySQL
Visualization: Microsoft Power BI
## Data Cleaning and Exploration🧹

Tools Used🛠️: Microsoft Excel

o Checked and formatted the cells with proper datatypes

Missing Values in each column
o used filter function in excel to identify missing/null values

o identifing Duplicates

o Handling the missing values by using find & select inbuilt function in excel
1. Replaced the blank space with NULL for the column that is TEXT Datatype

## Data Analysis 📈

Tools Used⚙️:MySQL

Creating and importing dataset to MySQL


```Mysql
Create Table census (
District varchar(50),
State varchar(100),
Growth Decimal(5,3),
Sex_Ratio int,
Literacy Decimal(5,3)
);
```

```Mysql
Create Table Geograph(
	District Varchar (100),
	State Varchar (100),
	Geo Int,
	Population int
);
```

o Selecting and viewing the dataset

```Mysql
SELECT * from census;

SELECT * from Geograph;
```
