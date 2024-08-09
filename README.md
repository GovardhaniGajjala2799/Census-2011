
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

 ## Total Columns
 
```mysql
Select * from geograph;

select * from census;
```

o Total Number of rows

```mysql
Select count(*) from census;
select count(*)from geograph;
```

o Total Districts

```mysql
Select Count(distinct(District)) Total_Districts from census;
```

o Total States

```mysql
Select Count(distinct(State)) Total_States from census;
```

o Total population of India

```mysql
select Sum(Population) from geograph;
```

o Average literacy rate of India

```mysql
with cte as (select round(avg(literacy)) literacy_of_India from census group by state)
select round(avg(literacy_of_India),2) from cte;
```

o Average Sex Ratio

```mysq
with cte as (select avg(Sex_Ratio) Sex_Ratio_of_India from census group by state)
select avg(Sex_Ratio_of_India) Sex_Ratio_of_India from cte;
```

o Average growth of india

```mysql
with cte as (select avg(Growth*100) growth_of_India from census group by state)
select round(avg(growth_of_India),2) from cte;
```

o Total area Of India

```mysql
with cte as (select sum(geo) Area_of_India from geograph group by state)
select sum(Area_of_India) from cte;
```

o Average Growth, average sex_ratio, average literacy rate, sum of population, area(sq.km) for all the states

```mysql
select c.state, round(avg(round(c.growth,1)*100),2) Avg_Growth, round(avg(c.sex_ratio)) Avg_Sex_Ratio, 
round(avg(c.Literacy),2) Avg_Literacy, sum(g.population) Population, sum(g.geo) 'Area(Sq.km)'
from census c 
join geograph g
on c.district = g.district
group by c.state
Order by Population desc;
```

o Top 10 states by literacy

```mysql
Select round(Avg(literacy)) Literacy, state from census
group by state
order by Literacy desc
limit 10; 
```

o Bottom 10 states by literacy

```mysql
Select round(Avg(literacy),2) Literacy, state from census
group by state
order by Literacy asc
limit 10; 
```

o  Top 5 states by growth rate

```mysql
Select state, round(avg(growth)*100,2) growth
from census 
group by state
order by growth desc
limit 5;
```

o Bottom 5 states by gowth rate

```mysql
Select state, round(avg(growth)*100,2) growth
from census 
group by state
order by growth asc
limit 5;
```

o Top 10 states by population

```mysql
Select state, sum(population) population
from geograph 
group by state
order by population desc
limit 10;
```

o Top 10 states by sex ratio

```mysql
select state, round(Avg(sex_ratio)) Average_Sex_Ratio from census
group by state
order by Average_Sex_Ratio desc
limit 10;
```

o Bottom 10 states by population

```mysql
select state, round(Avg(sex_ratio)) Average_Sex_Ratio from census
group by state
order by Average_Sex_Ratio
limit 10;
```

o PRVIOUS YEAR POPULATION

```mysql
with cte as (select c.District, c.state, c.Growth, g.population 
from census c join geograph g 
on c.district = g.District)
select district, state, round((Population/(growth+1))) Population_Before, population Population_After from cte
order by state;
```

o Males and females of states according to Census 2011

```mysq
with cte as(select c.district,
c.state, c.sex_ratio/1000 as sex_ratio1, g.population 
from census c join 
geograph g 
on c.district = g.district), cte2 as
(select district, state ,population, round(population/(sex_ratio1 +1),0) as males , 
round((population * sex_ratio1)/(sex_ratio1 +1),0) as females from cte order by state, district)
select state, sum(males) as population_male, sum(females) as population_females from cte2 
group by state;
```
