# PROJECT_GOING_SOMEWHERE
## PROJECT OVERVIEW
<span style="color: #222222;">The latest update from Word Tourism Organization (UNWTO) in December 2020 stated: “the decline in the first ten months of 2020 represents 900 million fewer international tourist arrivals compared to the same period in 2019, and translates into a loss of US</span> <span style="color: #222222;">$</span><span style="color: #222222;">935 billion in export revenues from international tourism, more than 10 times the loss in 2009 under the impact of the global economic crisis”</span>
In 2021, the Research department of the World Tourism Organisation requested a synthesis report of the global tourism trends in 2021

## OBJECTIVE OF THIS STUDY 
The main objective of the report was to undertsand the tourism data by country analysis and study the trend of expenditure and visits between 2020 and 2021. 
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
1. How is the expenditure situation for countries between 2020 and 2021?
2. Did Tourism/ visitors rise or fall between 2020 and 2021
3. Take a closer look at data from America and France. 
## DATA ANALYSIS
```SQL

--General table overview
SELECT *
FROM main.Tourism_in_countries


--Tourism expenditure (millions of US dollars) in 2020 and 2021 by country (Which countries are spending more in tourism in 2021)
SELECT Tourism_in_countries.Location, Tourism_in_countries.Year, Tourism_in_countries.Value
FROM Tourism_in_countries
WHERE Year >= 2020
  and "Series " = "Tourism expenditure (millions of US dollars)"
order by Location



--Tourism/visitor arrivals (thousands) in 2020 and 2021 by country
SELECT Tourism_in_countries.Location, Tourism_in_countries.Year, Tourism_in_countries.Value, Tourism_in_countries."Series "
FROM Tourism_in_countries
WHERE "Series " = 'Tourist/visitor arrivals (thousands)'and Year >= 2020
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


--only USA data
select Tourism_in_countries.Location, Tourism_in_countries.Value, Year, "Series "
from Tourism_in_countries
where Location = 'United States of America'
order by Value
```

## Findings
From careful analysis of the charts, it was understood that 
1. Between 2020 and 2021, many countries (89%) increased their expenditure on Tourrism, as 2021, was the year that saw a more relaxed post Covid regulations in several couyntries. Although the United States of America was the only country in the top 10 to reduce their expenditure on tourism.
2. The sitaution of USA could be as a result of the sharp fall in tourists/visitors between 2019 and 2020, and a little steady rise in the numbers for 2021. On the other hand, France, did experience a sharp fall in tourists/visitirs between 2019 and 2020 and a steady rise in the numbers in 2021, but did increase their expenditure on tourism by about 15%.
3. In general, global tourism steadly rose between 2020 and 2021, although that did not correspond to the growth in expenditure in tourism. 

## SUMMARY
To summerise, many countries in the world increased their expenditure for tourism between 2020 and 2021, although in most of these countries, the number of visitors or tourists has fallen drastically due to the aftermath of the pandemic and its subsequent lockdown protocols. 




      
