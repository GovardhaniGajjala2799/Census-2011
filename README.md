
# India Population Census 2011 Analysis

## INTRODUCTION

The 2011 Census of India is a comprehensive dataset that provides a wealth of information on the demographic, social, and economic characteristics of the country. As a decennial exercise, the Census serves as a crucial benchmark for measuring India's progress and development across various indicators. This project aims to leverage the insights gleaned from the 2011 Census data to generate actionable intelligence that can inform policymaking, resource allocation, and strategic planning at the national and subnational levels.

## Data Exploration and Cleaning

The dataset includes information on various metrics such as population, literacy rate, sex ratio, growth rate, and geographical area at the state and district levels. The data was first inspected for any missing values or inconsistencies, and necessary cleaning was performed to ensure data integrity.

## Tools Used 🛠️

Database: MySQL
Visualization: Microsoft Power BI

## Data Cleaning and Exploration🧹

Tools Used🛠️: Microsoft Excel

o Checked and formatted the cells with proper datatypes

![Screenshot (23)](https://github.com/user-attachments/assets/1b3f0efe-60c5-4938-9b52-7bf16b197157)

Missing Values in each column
o used filter function in excel to identify missing/null values

![Screenshot (37)](https://github.com/user-attachments/assets/1d81baf4-6432-40d1-950e-330d947a0485)

o identifing Duplicates
o Handling the missing values by using find & select inbuilt function in excel
1. Replaced the blank space with NULL for the column that is TEXT Datatype

![Screenshot (24)](https://github.com/user-attachments/assets/51f3f1f7-78a1-47b3-a4b0-21eaaa788219)

## Data Analysis 📈

Tools Used⚙️:MySQL

o Creating and importing dataset to MySQL

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
![fd](https://github.com/user-attachments/assets/518a3fe0-52c2-4eae-a3b5-439c2cc33d54)

o Total Number of rows

```mysql
Select count(*) from census;
select count(*)from geograph;
```
![Screenshot (26)](https://github.com/user-attachments/assets/74bdf362-495d-4d7b-90b5-aaf9bcf9cda2) ![Screenshot (26)](https://github.com/user-attachments/assets/74bdf362-495d-4d7b-90b5-aaf9bcf9cda2)

o Total Districts

```mysql
Select Count(distinct(District)) Total_Districts from census;
```
![Screenshot (26)](https://github.com/user-attachments/assets/dbf6f070-b0cd-4243-bf84-92c9ee28c4a0)

o Total States

```mysql
Select Count(distinct(State)) Total_States from census;
```
![Screenshot (27)](https://github.com/user-attachments/assets/545adabb-1200-473d-8350-abd400fc7a34)

o Total population of India

```mysql
select Sum(Population) from geograph;
```
![Screenshot (28)](https://github.com/user-attachments/assets/836c480d-8710-498a-bee7-26ff03bdb4f5)

o Average literacy rate of India

```mysql
with cte as (select round(avg(literacy)) literacy_of_India from census group by state)
select round(avg(literacy_of_India),2) from cte;
```
![th](https://github.com/user-attachments/assets/c32e46cf-1a91-4fdd-ba19-bafc25916eae)

o Average Sex Ratio

```mysq
with cte as (select avg(Sex_Ratio) Sex_Ratio_of_India from census group by state)
select avg(Sex_Ratio_of_India) Sex_Ratio_of_India from cte;
```
![Screenshot (38)](https://github.com/user-attachments/assets/99fd8581-a5e3-4b79-be67-81518b9d9c4b)

o Average growth of india

```mysql
with cte as (select avg(Growth*100) growth_of_India from census group by state)
select round(avg(growth_of_India),2) from cte;
```
![Screenshot (41)](https://github.com/user-attachments/assets/0b8abff2-0621-4c81-bc3f-7e6b4a1b957d)

o Total area Of India

```mysql
with cte as (select sum(geo) Area_of_India from geograph group by state)
select sum(Area_of_India) from cte;
```
![Screenshot (31)](https://github.com/user-attachments/assets/a8bf80d5-f5f2-4ce8-b15e-95c0c8d16668)

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
![Screenshot (32)](https://github.com/user-attachments/assets/6b18e365-589c-41b3-a05b-a6ab04badafb)

o Top 10 states by literacy

```mysql
Select round(Avg(literacy)) Literacy, state from census
group by state
order by Literacy desc
limit 10; 
```
![Screenshot (33)](https://github.com/user-attachments/assets/12cfd3cd-30e3-45fe-862c-0c15623279cb)

o Bottom 10 states by literacy

```mysql
Select round(Avg(literacy),2) Literacy, state from census
group by state
order by Literacy asc
limit 10; 
```
![Screenshot (34)](https://github.com/user-attachments/assets/375a54ce-c828-4e39-9c85-33ee9193693e)

o  Top 5 states by growth rate

```mysql
Select state, round(avg(growth)*100,2) growth
from census 
group by state
order by growth desc
limit 5;
```
![gro](https://github.com/user-attachments/assets/6e906a24-d410-4f10-8cb2-77fc22d56aa6)

o Bottom 5 states by gowth rate

```mysql
Select state, round(avg(growth)*100,2) growth
from census 
group by state
order by growth asc
limit 5;
```
![Screenshot (35)](https://github.com/user-attachments/assets/c25c69f5-75e3-4c46-a54e-4b0ac3aa41a2)

o Top 10 states by population

```mysql
Select state, sum(population) population
from geograph 
group by state
order by population desc
limit 10;
```
![pop](https://github.com/user-attachments/assets/33603f95-b8a1-4dfb-ad65-a37ba14b1308)

o Top 10 states by sex ratio

```mysql
select state, round(Avg(sex_ratio)) Average_Sex_Ratio from census
group by state
order by Average_Sex_Ratio
limit 10;
```
![topsexratio](https://github.com/user-attachments/assets/1395171f-9203-4416-b1c4-50b3f5a13138)

o PRVIOUS YEAR POPULATION

```mysql
with cte as (select c.District, c.state, c.Growth, g.population 
from census c 
join geograph g 
on c.district = g.District)
select state, sum(round((Population/(growth+1)))) Population_Before, sum(population) Population_After 
from cte 
group by state
order by state;
```
![bfrpop](https://github.com/user-attachments/assets/3211057a-a38f-4b90-af99-4c3530f2e47c)

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
![Male and Female1](https://github.com/user-attachments/assets/f5931c0a-fe1a-4777-8be9-14a74cb4a5a2)

## Data Visualization
Tools Used⚙️:Microsoft Power BI

![1](https://github.com/user-attachments/assets/cde6eca5-789f-4342-8860-a232bec0a85d)


## Descriptive Analysis(Findings)

a. __States by Population:__
The analysis reveals that Uttar Pradesh, Maharashtra, and Bihar are the most populous states in India, while Goa, Sikkim, and Nagaland have the smallest populations.

b. __States by Literacy Rate:__ 
Kerala, Delhi, and Himachal Pradesh have the highest literacy rates, while Rajasthan, Jharkhand, and Arunachal Pradesh have the lowest.

c. __States by Sex Ratio:__ 
Kerala, Pondicherry, and Andaman and Nicobar Islands have the highest sex ratios, while Daman and Diu, Dadra and Nagar Haveli, and Haryana have the lowest.

d. __States by Growth Rate:__ 
Dadar and Nagar Haveli, Daman and Diu, and Meghalaya have the highest population growth rates, while Nagaland, Kerala, and Goa have the lowest.

e. __Mapping Population Distribution:__
The population distribution across Indian states and districts was visualized using a geographic information system (GIS) to identify population hotspots and sparsely populated regions.

f. __Analyzing Regional Disparities:__ 
The data was used to investigate regional disparities in literacy rates, sex ratios, and growth rates. 
This analysis can inform targeted interventions to address these imbalances.

## Policy Implications

a. __Informing Resource Allocation:__ 
The insights from the analysis can guide the allocation of resources and the prioritization of government schemes across different states and districts based on their specific needs and developmental challenges.

b. __Evaluating Policy Effectiveness:__ 
The 2011 Census data can serve as a baseline for measuring the impact of policies and initiatives introduced after 2011, enabling policymakers to assess their effectiveness and make informed decisions for the future.

## Limitations and Future Scope

a. __Limitations:__ 
The analysis is based on the 2011 Census data, which may not capture the most recent demographic changes. Additionally, the data does not provide insights into socio-economic factors that could influence the observed trends.

b. __Future Scope:__ 
Future research can incorporate more recent data sources, such as the 2021 Census, to analyze the evolving demographic and socio-economic landscape of India. Additionally, cross-referencing the Census data with other datasets, such as economic indicators and social welfare metrics, could provide a more comprehensive understanding of India's development.

## Conclusion

The 2011 Census of India serves as a valuable resource for researchers, policymakers, and planners to gain insights into the country's demographic, social, and economic landscape. This project has demonstrated the potential of the Census data to support evidence-based decision-making and guide the formulation of effective policies and development strategies for India.
