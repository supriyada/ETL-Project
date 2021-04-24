# ETL-Project -- Youtube Channel statistics
## Summary:
As we all know, Youtube videos are getting popular day-by-day. There are lot of channels with videos for all ages and in all genres. As part of this project, I thought to explore the statistics of a very few of the channels and challenge my skills learned from bootcamp.<br>
A main jupyter notebook is maintained and all the function to extract is called from the main notebook. Later, all the loading into database is done in continuation to this.<br>

## Order of execution:
> - Please provide the google API key in api_keys.py <br>
> - Also provide mongodb cloud username & password in config.py <br>
> - api_calls --> this notebook calls the function to retreive data using youtube API key. I had stored the output I fetched into csv file. If you donot wish to run this, please proceed with next step.
> - <strong> main_notebook</strong> --> this notebook calls all other notebook and does the loading part into db & cloud.

## Datasets:
The data for the statistics is collected from various resources. To short list the number channels to collect the statistics, channel ids are collected from the publicly available dataset & by web scrapping. They are as follows,<br>
•	DataWorld<br>
•	Kaggle dataset<br> 
•	Youtube API<br>
•	Website: https://www.noxinfluencer.com/youtube-channel-rank/top-100-all-all-youtuber-sorted-by-subs-weekly<br>

## Database used: 
I wished to enrich my knowledge on NO SQL database. Hence, I chose MongoDB over POSTGRESQL [which I am familiar with]. After cleaning the data, all the details are stored as documents in collections within database name “youtube_db”. The data is also uploaded in the cloud with database name: “youtube_cloud_db”.<br>

## Libraries used:
•	import import_ipynb<br>
•	import pandas as pd<br>
•	from pymongo import MongoClient<br>
•	from webdriver_manager.chrome import ChromeDriverManager<br>
•	import requests<br>
•	from bs4 import BeautifulSoup as bs<br>
•	from selenium import webdriver<br>
•	import json<br>

### Extract:
> From the dataworld datasets, records are downloaded in CSV format “Channel_details.csv”. <br>
>	From the Kaggle datasets, “category_id.json” with the video category details are downloaded.<br>
>	The website: https://www.noxinfluencer.com/youtube-channel-rank/top-100-all-all-youtuber-sorted-by-subs-weekly is scrapped to get the top 100 youtube channels and stored in dictionary.<br>
>	Youtube developers’ data is queried with API key using the URL,<br>
https://youtube.googleapis.com/youtube/v3/channels?part=snippet&part=statistics&id={id}&key={g_key}<br>
### Tranform:
> The “category_id.json” is read using pandas and converted into dataframe. The snippet column has the category name and id is category id. Hence the remaining columns are dropped and required column is extracted.<br>
> The “Channel_details.csv” has 26 columns. Of all the columns 5 columns are extracted.<br>
> The website: https://www.noxinfluencer.com/youtube-channel-rank/top-100-all-all-youtuber-sorted-by-subs-weekly is scrapped and channel details are collected. Since the website infinite scrolling functionality, I used selenium driver and BeautifulSoup to scrape the website. In the final output there was space in the beginning and end of each value in the columns. They are stripped to make it data usable.<br>
> Now that we have the channel id from the dataset in csv file and from scrapped date, youtube API is queried and the statistics details are collected.
URL: https://youtube.googleapis.com/youtube/v3/channels?part=snippet&part=statistics&id={id}&key={g_key}<br>
### LOAD:
> The database connection is made:    <br>
> The database “youtube_db” is created.<br>
> The collections are created and inserted the data retrieved from all four sources<br>
> The data is also loaded into the cloud. <br>

## SUMMARIZE:
	The ETL is performed on the data. With the data from dataset [dataworld & Kaggle], API and web scrapping, channel Id are retrieved and with the help of that statistics of individual channel is obtained. <br>




