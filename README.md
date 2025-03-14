# Analysis of Campaign Performance Using SQL

## Table of Contents
- [Introduction](#Introduction)
- [Objectives](#Objectives)
- [Tools](#Tools)
- [Data Source](#Data-Source)
- [Data Understanding](#Data-Understanding)
- [Analysis &  Query Writing](#Analysis-&-Query-Writing)
- [Conclusion](#Conclusion)
## Introduction
###### In the competitive landscape of digital marketing, companies are increasingly leveraging data to fine-tune their advertising strategies and maximize their return on investment (ROI). This report explores the performance of digital advertising campaigns across various platforms using SQL to analyze key metrics. By assessing variables such as impressions, clicks, conversion rates, acquisition costs, and ROI, we aim to uncover patterns that can help improve campaign performance. Through this analysis, we will provide valuable insights on optimizing ad spend, identifying high-performing channels, and determining the most cost-effective campaigns.

## Objectives
###### 1.	To familiarize with the dataset, review its structure, and identify key variables crucial for analyzing digital marketing campaigns.
###### 2.	To calculate essential metrics like click-through rates (CTR), total impressions, conversions, and cost per conversion, allowing for performance evaluation.
###### 3.	To rank campaigns by their effectiveness, focusing on ROI, conversion rates, and engagement scores to determine the most successful campaigns.
###### 4.	To identify the top-performing channels by analyzing total conversions and impressions, providing a clear understanding of the most effective advertising platforms.
###### 5.	To evaluate and compare the cost-effectiveness of campaigns to ensure optimal budget allocation and maximize returns.
###### 6.	To provide actionable recommendations based on the data analysis to enhance future digital marketing strategies.


## Tools
###### The following tools were used for data retrieval, analysis, and documentation:
###### •	Microsoft Excel for storing the dataset
###### •	PostgreSQL for SQL query execution.
###### •	Google Drive for storing SQL scripts and reports.

## Data Source
###### As part of my internship at HNG, I was supplied with a [Marketing Campaign Dataset](https://docs.google.com/spreadsheets/d/1LBGqmX9jT6HuJwHrVZXjIKPxqElkYFPg/edit?gid=751358393#gid=751358393) in CSV format. To better understand the data, I first loaded it into SQL for exploration and analysis. This step allowed me to familiarize myself with the dataset structure, identify key metrics, and prepare for deeper insights. The goal of my analysis is to extract actionable insights that will guide stakeholders in optimizing their marketing strategies and ad spend.

## Data Understanding
Firstly I had to create a table in PostgreSQL called campaigndata to house my data and define the data types for the columns.
![Create table](https://github.com/OKUNDALAYE/SQL-Analysis-Portofolio/blob/main/assets/images/Create%20table.PNG)

 Then I imported the data in SQL.
After that, I had to review and inspect the dataset structure to understand available fields and data types and ensure that the data types (e.g., numeric, text, date) are appropriate for analysis.
 Based on the sample data provided and the available fields in the dataset, here's an overview:
The dataset includes the following columns:
1.	Company (Text): Name of the company running the campaign.
2.	Campaign_Type (Text): The type of campaign (e.g., Email, Display, Social Media).
3.	Target_Audience (Text): Demographic targeting for the campaign (e.g., Men 18-24, Women 35-44).
4.	Duration (Text): The duration of the campaign (e.g., 30 days, 60 days).
5.	Channel_Used (Text): The advertising channel/platform used (e.g., Google Ads, YouTube, Instagram).
6.	Conversion_Rate (Numeric): The conversion rate for the campaign, a decimal number (e.g., 0.04).
7.	Acquisition_Cost (Money): The total cost of acquiring customers through the campaign, in monetary units (e.g., $16,174.00).
8.	ROI (Numeric): Return on Investment (ROI) for the campaign, expressed as a numeric value (e.g., 6.29).
9.	Location (Text): Geographic location where the campaign was targeted (e.g., Chicago, New York).
10.	Date (Date): The date when the campaign started (e.g., 1/1/2021).
11.	Clicks (Integer): The total number of clicks generated by the campaign.
12.	Impressions (Integer): The total number of impressions generated by the campaign.
13.	Engagement_Score (Integer): A numeric score representing engagement for the campaign (e.g., 6, 7, 10).
14.	Customer_Segment (Text): The specific customer segment targeted by the campaign (e.g., Health & Wellness, Fashionistas).

The key variables I’ll be focusing on for my analysis are:
1.	Impressions (Integer):
o	Represents the number of times an ad is shown to users. This is essential for calculating metrics like CTR (Click-Through Rate) and evaluating the reach of campaigns.
2.	Clicks (Integer):
o	Represents the number of times users clicked on the ad. This, combined with Impressions, is critical for calculating CTR and understanding campaign engagement.
3.	Conversion_Rate (Numeric):
o	Indicates the proportion of clicks that result in a desired outcome (e.g., purchase, sign-up). This helps assess campaign effectiveness in driving action.
4.	Acquisition_Cost (Money):
o	Reflects the cost incurred for acquiring each customer or conversion. This is key to evaluating the cost-effectiveness of campaigns.
5.	ROI (Numeric):
o	Reflects the return generated from the investment in a campaign. Analyzing ROI is essential for understanding the profitability of campaigns.

## Analysis &  Query Writing 
##### The following are questions that will guide my analysis and how I use SQL to extract insights from my data:
##### 1.	Calculate Total Impressions for Each Campaign
```sql
SELECT campaign_id, SUM(impressions) AS totalimpressions
FROM campaigndata
GROUP BY campaign_id
ORDER BY totalimpressions DESC;

```
 
###### There were 200,005 campaigns that were run in the data, that’s a lot of campaigns and 10,000 impressions was the highest impressions gotten.

2.	Identify the Campaign with the Highest ROI
```sql
SELECT campaign_id, company, roi
FROM campaigndata
ORDER BY ROI DESC
LIMIT 1;

```
 
###### Campaign with the Id 168 had the highest ROI(Return on Investment) at 800% and the company that ran that campaign is NextGen Systems. This means that for every $1 spent, the campaign generated $8 in return.
3.	Find the Top 3 Locations with the Most Impressions
```sql
SELECT location, SUM(impressions) AS totalimpressions
FROM campaigndata
GROUP BY Location
ORDER BY totalimpressions DESC
LIMIT 3;
```
 
###### New York is the location with the highest Impressions at 221.35 million impressions followed by Miami with 221.34 million impressions and Chicago is the least of the top 3 locations with 219 million impressions.

4.	Calculate Average Engagement Score by Target Audience
```sql
SELECT target_audience, AVG(engagement_score) AS avgengagementscore
FROM campaigndata
GROUP BY target_audience
ORDER BY avgengagementscore DESC

```
 
###### On average, Men between 18-24 have the highest average engagement score (5.5150), meaning they interact the most with the marketing campaigns.
 ###### Women between 25-34 come next with an engagement score of 5.4927, closely followed by Men 25-34 at 5.4918.
###### All other ages group have an engagement score of 5.4868, suggesting that the overall audience has a relatively high interaction rate.
###### Women between 35-44 have the lowest engagement score among the top five, at 5.4865, but the difference between groups is minimal

5.	Calculate the Overall CTR (Click-Through Rate)
   ```sql
SELECT (SUM(clicks) * 100.0) / SUM(impressions) AS overallctr
FROM campaigndata;

```
 
###### This indicates that for every 100 impressions, roughly 9.98 users clicked on the ad. This is a solid Click Through Rate, suggesting that the ads are relatively effective at driving user interaction compared to the industry average, where CTRs tend to hover around 2-3% for most digital platforms.

6.	Find the Most Cost-Effective Campaign
```sql
SELECT campaign_id, company, 
    (CAST(REPLACE(REPLACE(acquisition_cost::TEXT, '$', ''), ',', '') AS NUMERIC) / (conversion_rate * clicks)) AS costperconversion
FROM campaigndata
ORDER BY costperconversion ASC;

```
 
###### Campaign with id 118451 from Alpha Innovations has the lowest cost per conversion at $34.22 which makes it thee most cost effective campaign.
###### This means that for every successful conversion, Alpha Innovations spent approximately $34.22, making it the most efficient campaign.
###### Alpha Innovations has three campaigns in the top six most cost-effective campaigns, 3 of the campaigns they ran were among the most cost effective. 

7.	Find Campaigns with CTR Above a Threshold
```sql
SELECT 
    campaign_id, 
    company, 
    (SUM(clicks) * 100.0) / SUM(impressions) AS ctr
FROM campaigndata
GROUP BY campaign_id, company
HAVING (SUM(clicks) * 100.0) / SUM(impressions) > 5
ORDER BY ctr DESC;

```
 
###### Campiagn with id 123375 had the highest click through rate at 99.2%. The top 10 campaigns shown have extremely high CTRs, ranging from 99.2% down to 96.9%. This suggests that these campaigns were very effective at getting people to click. 
###### TechCorp appear 2 times and Alpha Innovations appear 3 times in the top 10, indicating they are running highly effective campaigns that generate high click-through rates.

8.	Rank Channels by Total Conversions
```sql
SELECT
    channel_used,
    SUM(clicks * conversion_rate) AS totalconversions
FROM campaigndata
GROUP BY channel_used
ORDER BY totalconversions DESC;

```
 
###### Email has the highest number of total conversions (1,485,393.65) and is ranked 1st. 
###### Website and Google Ads have very similar total conversions and are ranked 2nd and 3rd, respectively. 
###### YouTube and Instagram also have close total conversion numbers and are ranked 4th and 5th. 
###### Facebook has the lowest number of conversions among the displayed channels and is ranked 6th.
###### Email, Website, and Google Ads are the most effective channels for driving conversions.

## Conclusion
###### The analysis of the 200,005 campaigns provides valuable insights into the effectiveness of various digital marketing efforts. Key findings indicate that NextGen Systems achieved the highest Return on Investment (ROI) at 800%, demonstrating strong revenue generation. In terms of reach, New York, Miami, and Chicago led in impressions, with over 219 million impressions each.
###### Engagement trends revealed that men aged 18-24 had the highest interaction with ads, closely followed by women aged 25-34. Overall, the audience engagement scores were consistently high across all age groups. The overall Click-Through Rate (CTR) stood at 9.98%, significantly exceeding industry averages, highlighting strong user interest in the ads.
###### Cost-effectiveness analysis identified Alpha Innovations as the top performer, with a cost per conversion of $34.22. Additionally, TechCorp and Alpha Innovations ran some of the highest CTR campaigns, exceeding 96.9%, proving their ability to drive clicks effectively.
###### Finally, Email emerged as the top channel for conversions, followed by Website and Google Ads, emphasizing the importance of direct marketing and search-driven strategies. Facebook, while ranking lowest in conversions, still played a role in the overall digital marketing mix.
###### These insights offer a strategic direction for optimizing future campaigns by prioritizing high-performing channels, refining audience targeting, and leveraging cost-efficient strategies to maximize ROI and engagement.





