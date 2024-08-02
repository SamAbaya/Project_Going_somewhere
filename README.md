# PROJECT_GOING_SOMWEHERE
## PROJECT OVERVIEW
<span style="color: #222222;">The latest update from Word Tourism Organization (UNWTO) in December 2020 stated: “the decline in the first ten months of 2020 represents 900 million fewer international tourist arrivals compared to the same period in 2019, and translates into a loss of US</span> <span style="color: #222222;">$</span><span style="color: #222222;">935 billion in export revenues from international tourism, more than 10 times the loss in 2009 under the impact of the global economic crisis”</span>
In 2021, the Research department of the World Tourism Organisation requested a synthesis report of the globalk touriosm trends in 2021

## OBJECTIVE OF THIS STUDY 
The main objective of the report was to undertsand the tourism data by country analysis and to extablish which countriues are seeing the greatest fall in tourism numbers. 
## DATA SOURCE
UNWTO Tourism dataset (Attached to files)
## TOOLS
  - Microsoft Excel for data cleaning 
  - Jetbrain DataGrip for data query and analysis [Download Here](https://www.jetbrains.com/datagrip/download/#section=mac)
  - Tableau for data visualisation and report [Download Here](https://identity.idp.tableau.com/login?state=hKFo2SByZG9HdTE2aTBiZ1k5MkhYcmI5TTN6aFY0dEx5Y2dwdqFupWxvZ2luo3RpZNkgbmhIQ3pRTGNiV1k5R0tkYUZQZ09TWGYya3JTWW53dG2jY2lk2SB3Y1M3SHdZOThxZGZnQlJFSFQ3WG9sbjdpcGM3NVUwYQ&client=wcS7HwY98qdfgBREHT7Xoln7ipc75U0a&protocol=oauth2&response_type=code&redirect_uri=https%3A%2F%2Fpublic.tableau.com%2Fpublic%2Fapis%2Fauth%2Fprovision&scope=openid%20email%20profile&nonce=CnyFHKrnLoM)
## DATA CLEANING AND PREPARATION
During the data cleaning phase, the following tasks were performed
  1. Data loading into excel and inspection
  2. Handling missing values and spelling errors
  3. Formatting the file for subsequent uoloading into DataGrip SQL management system
## DATA EXPLORATION
The exploration of the data was geared towards answering questions such as 
1. What countries have reduced their tourism expenditures post Covid lockdown?
2. Did Tourism/ visitors rise or fall in 2021 and by what margin?
3. Which countries are seeing a rise in tourism numbers and which areas are experiemncing a decline in the numbers.
## DATA ANALYSIS
```SQL

--General table overview
SELECT *
FROM main.Tourism_in_countries

--Tourism expenditure (millions of US dollars) in 2021 by country (Which countries are spending more in tourism in 2021)
SELECT Tourism_in_countries.Location, Tourism_in_countries.Year, Tourism_in_countries.Value
FROM Tourism_in_countries
WHERE Year = 2021
group by Location
order by Value;

--Tourism expenditure (millions of US dollars) in 2020 by country (Which countries are spending more in tourism in 2021)
SELECT Tourism_in_countries.Location, Tourism_in_countries.Year, Tourism_in_countries.Value
FROM Tourism_in_countries
WHERE Year = 2020
group by Location
order by Value;

--Tourism/visitor arrivals (thousands) in 2021 by country
SELECT Tourism_in_countries.Location, Tourism_in_countries.Year, Tourism_in_countries.Value, Tourism_in_countries."Series "
FROM Tourism_in_countries
WHERE "Series " = 'Tourist/visitor arrivals (thousands)'and Year = 2021
group by Year, Location
order by Value;

--Tourism/visitor arrivals (thousands) in 2020 by country
SELECT Tourism_in_countries.Location, Tourism_in_countries.Year, Tourism_in_countries.Value, Tourism_in_countries."Series "
FROM Tourism_in_countries
WHERE "Series " = 'Tourist/visitor arrivals (thousands)'and Year = 2020
group by Year, Location
order by Value;

--Tourism/visitor arrivals (thousands) in 2021 and 2020 by country
SELECT Tourism_in_countries.Location, Tourism_in_countries.Year, Tourism_in_countries.Value, Tourism_in_countries."Series "
FROM Tourism_in_countries
WHERE "Series " = 'Tourist/visitor arrivals (thousands)'and Year >=2019
group by Year, Location
order by Location;

--Data from france only
with Tic as (select location, year, "Series ", Value
      from Tourism_in_countries
      where Location = 'France' and 'Series'= 'Tourist/visitor arrivals (thousands)'
group by location, year, "Series ", Value
order by Year)
select *
from Tic
WHERE Location='France'

--only France data
select Tourism_in_countries.Location, Tourism_in_countries.Value, Year, "Series "
from Tourism_in_countries
where Location = 'France'
order by Value

select Tourism_in_countries.Year, Tourism_in_countries.Value
from Tourism_in_countries
where Year = '1995'
group by Year, Value
```
[DASHBOARD](dashboard)






      
