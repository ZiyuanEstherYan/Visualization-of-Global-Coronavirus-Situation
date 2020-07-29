# Visualization of Global Coronavirus Situation
The project contains two interactive dashboards in total, one for observations of COVID-19 in the U.S. and one for those at a worldwide scale. To convey detailed and organized information of confirmed cases and deaths in a more vivid way, both the dashboards are designed to have a map at the center. Users can explore more by themselves by playing with the maps. 

### Tool: Tableau

## Introduction
On December 31, 2019, the World Health Organization’s (WHO’s) China Country Office received information that a pneumonia of unknown cause had infected patients in the city of Wuhan. Less than two months later, on February 11, the WHO named this disease COVID-19. This disease was identified as a novel coronavirus, and at that point, had spread through many provinces of China while taking a heavy toll on its economy. It took another month before COVID-19 had taken its foothold in the United States, with California becoming the first state in the US to put a shelter in place order into effect on March 20. COVID-19 is something that has affected the lives of most of us on some degree, and will continue to for some time. With the advances and increased access to data science/visualization tools, many data practitioners have used the tools at their disposal to create insightful visualizations and predictions about COVID-19. Using some popular visualizations as inspiration, our group sought Tableau to create an interactive tool to help individuals better understand the progression of this disease, as well as take the necessary precautions.

After examining the data, we created a plan for the creation of our dashboards. Since there were two types of data (time series, daily summary), we felt that the best course of action was to create two separate dashboards: one for United States’ cases and one for worldwide cases. After creating the dashboard, we decided we would aggregate the data by continent, and display the progression of COVID-19 by countries within each continent. This dashboard can be used to learn from the data that has been collected and minimize the damage the COVID-19 can potentially cause. 

## Data
The COVID-19 dataset we used can be found on the Tableau coronavirus portal, and is updated daily to reflect the constant flow of new cases that are reported worldwide. The dataset itself contains both deaths and confirmed cases per country and state/province if applicable. Every time the dataset is updated, a new entry is created for each country rather than deleting the previous entries. For this reason, aggregation is necessary to get the total numbers for the visualizations. Finally, the data was split into two types: time series and daily summary. Entries tagged as “time series” represented worldwide data, while “daily summary” data only concerns cases in the United States. The first time series data was collected on January 22, while the daily summary table was first created on March 24 as the researchers were hoping to create an aggregated view of United States COVID-19 cases. 

## Data Preparation
While we hoped to create two separate dashboards, the time series and daily summary data was contained within the same dataset. Before splitting the data, some cleaning steps were necessary since the two table types share the same fields. First, some extra fields such as Prep_Flow_Runtime, FIPS, Combined_Key, and Admin2 were removed. These attributes would not be necessary for our visualizations and removing them would improve the efficiency of our prep flow/visualization. At this point, we could split the dataset by the Table_Name attribute, and two tables were created. While the United States table was ready, our worldwide dashboard would require some external data. The worldwide data uses both Table_Name attributes as from March 23rd, US has not aggregated data in the time series, this way we can aggregate the US data for the US worldwide view.

For the worldwide COVID-19 views, we hoped to factor in per-capita cases. In order to make this calculation, we needed external population data for each country in our original dataset. To do this, we used the UN population data/estimates. This introduced a couple of new problems, since the UN data contained 2019 data as well as population projections through 2050, and some of the country names had different naming conventions than our original dataset. Unfortunately, this part of the data cleaning process required a bit of manual work as we had to replace the formal names of each country with their shorter/abbreviated names to join the two datasets. Since the UN data was collected in 2019, the data for 2020 was a prediction. For this reason we used 2019 population data for our per capita calculation, as we felt actual data would provide us with a reliable result compared to a prediction. For this reason, we excluded all population data not from the year 2019 and joined the population and COVID-19 by country name. Finally, we divided the population counts by 1000 since the data was in the 1000s. This is because calculating per capita infections is more meaningful at the actual scale of population. At this point, both of our datasets were ready and we could begin creating our dashboards.

## Dashboard Creation
### Dashboard 1:  COVID-19 Cases in the U.S.
This dashboard is composed of six views. The first two on the upper left are the billboards showing total numbers of confirmed cases and deaths. This allows the users to have a plain and straight impression of the current situation. And the two views that catch users’ eyes the most at the first glance would be the two maps at the center of the dashboard.

![alt_text](images/pic1.png "Pic 1")

The U.S. on the left is a tool created for users to easily click on states they are interested in and have an overall view of how the number of cases vary by states. The darkest blue lump, which is New York State, refers to a biggest number of confirmed cases, up until April 1. And the map on the right serves as a more detailed showcase which is connected to the U.S. map.

![alt_text](images/pic2.png "Pic 2")

For example, if users want to know details of a specific state in California, he or she could simply click California on the U.S. map and then the map beside it will jump to a bigger view of California with more detailed information. It is comparable by sight to tell which part of California is suffering the most confirmed cases.
At the half bottom of the dashboard, users can search for exact numbers by using the table. The table is also shown in a color grid, which helps users easily identify states with more serious situations. Also, a line chart is displayed to show the number of confirmed cases and deaths growing by time. Note that the starting date of our chart is March 24, when the original data sourced started to deliver U.S. specific data.

![alt_text](images/pic3.png "Pic 3")

### Dashboard 2: Worldwide Spread of COVID-19
As it is extremely likely that users who care about COVID-19 will want to also have a look at global situations and do some research, a dashboard with more useful functions is created. 

![alt_text](images/pic4.png "Pic 4")

At the upper half part, a world map with different sizes and colors of circles as well as territory is presented. This time, users can not only check the total number of cases in each country, but also see how many cases per capita are there in each country. Taking the USA as an example, the white color all over it indicates that its number of cases per capita is higher than the global average and the total number has reached the top 1. Users can also select a specific date they are interested in.
At the bottom half, to begin with is a similar grow trend chart. And on the right is a cross-country comparison chart with each country indicated by a color line. To not to mislead users, the starting point is set to be 1k, rather than 0 or 100. As it can be clearly seen that some countries like the USA and Italy are experiencing a steep growth curve while some countries like China and South Korea have become stable.

![alt_text](images/pic5.png "Pic 5")

### Story
Due to the importance of the growth rate of COVID-19 cases, we also built a story with a line of continents. Users can clearly see how COVID-19 cases develop among different countries in each continent. 

![alt_text](images/pic6.png "Pic 6")

First, a worldwide chart which is a mix of all countries that could be tracked is presented. By clicking at the dropdown menu on the upper right, users can manually select a specific continent. Or, they could follow the storyline at the top of the page.

![alt_text](images/pic7.png "Pic 7")

Then, following the story line, say, users now come to Europe. It is shown that almost all countries in Europe have a similar development trend of confirmed cases of COVID-19. This is also consistent with the fact that European countries are connected with each other closely. So, a probable projection will be that countries in Europe that just started to report confirmed cases will experience a similar path as other European countries.

## Conclusion
With the advent of data visualization tools in recent years, the potential for creating visualizations to drive the insight/understanding of this complex situation has greatly increased. We hope that these dashboards and story visualization can be helpful for individuals and decision makers alike, as COVID-19 continues to take its toll on the world. While many countries have taken a great sacrifice, others should use the mistakes/lessons learned from previous outbreaks to better prepare themselves, and there is no better way to drive this learning process than with data. 
