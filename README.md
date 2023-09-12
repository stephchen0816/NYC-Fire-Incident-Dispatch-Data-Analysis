# NYC-Fire-Incident-Dispatch-Data-Analysis
## Introduction

The purpose of this project is to ingest, analyze, and visualize the Fire Dispatch Data (https://dev.socrata.com/foundry/data.cityofnewyork.us/8m42-w767) by applying EC2 and Elasticsearch.
A python script was also used to run in the docker and to push the data into an OpenSearch cluster provisioned via AWS. 
Due to the size of the dataset, a python client of the Socrata API was used in order to load all the data into an Elasticsearch (OpenSearch) instance, and visualize/analyze with OpenSearch Dashboards. 
BulkAPI and various environmental variables were inputted through the terminal in order to achieve the best results. The data was cleaned as well to provide accurate results. The project analyzed around 5.6 million unique records.
4 visualizations were created using Kibana to answer the questions below:
*	What is the maximum amount of engines sent to each borough?
*	What are the top 10 highest max incidents at each borough?
*	What is the top 10 highest average engines assigned to each incident?
*	What is the top 10 longest average dispatch response to an incident?

The below are the commands used for the docker. 

Command to build docker image:
> docker build -t bigdataproject1:1.0 .

Command to run docker image:
> docker run -e INDEX_NAME="fire" -e DATASET_ID="8m42-w767" -e APP_TOKEN="0cGlnXvj7GthjtYxVQFr32BCV" -e ES_HOST="https://search-cis9760-project1-2d6s2yayjgaz45abz77sknlixy.us-east-2.es.amazonaws.com" -e ES_USERNAME="schen" -e ES_PASSWORD="Cis9760!" bigdataproject1:1.0 --page_size=30000 --num_pages=200

Below is the gauge chart of the number of rows uploaded:
![gauge](https://github.com/stephchen0816/NYC-Fire-Incident-Dispatch-Data-Analysis/assets/144307777/23ed348f-1ecf-4211-a11c-4e8e160be355)
## Analysis

**What is the maximum amount of engines sent to each borough?**
![visual01](https://github.com/stephchen0816/NYC-Fire-Incident-Dispatch-Data-Analysis/assets/144307777/1cfb1916-79e4-43ec-9701-5648ef5c3827)
The graph above visualizes the max amount of engines assigned to each borough. Here we see that in Brooklyn, the amount of engines they have been assigned is over 160 engines and Manhattan with 120 engines, while the other engines have around 80 engines or less. This is surprising because Manhattan has significantly more residents than Brooklyn does. The number of fire trucks can impact the response time they have to upcoming incidents. 

**What are the top 10 highest max incidents at each borough?**
![visual02](https://github.com/stephchen0816/NYC-Fire-Incident-Dispatch-Data-Analysis/assets/144307777/d483d0f7-adf6-450d-8e90-51c07adb892f)
The graph above visualizes the top 10 max incidents coded into the data by borough. Unfortunately, Kibana UI cuts off the legend in the upper right corner. Based on this graph, Brooklyn appears to have the most incidents overall. This is slightly surprising due to Manhattan having significantly  more residents. However, unexpectedly, most of the incidents are due to various utility emergencies (such as water,  gas, steam, electric, etc). The other incidents are classified as vehicle accidents, untenanted fires, and unidentified emergencies. This graph indicates the different types of incidents firefighters are called for at each borough. This data should be taken into consideration in how to avoid these types of incidents. 

**What is the top 10 highest average engines assigned to each incident?**
![visual03](https://github.com/stephchen0816/NYC-Fire-Incident-Dispatch-Data-Analysis/assets/144307777/d2950cfd-a247-4c54-a4b7-27a0813c4dbe)
The graph above visualizes the top 10 highest average engines assigned per incident. This data indicates what incidents are using the most resources. All of the incidents are assigned to fires but in different types of buildings, most are from untenanted buildings. This is interesting as more firetrucks are being used for untenanted buildings as I would have thought that more engines would be assigned to tenanted buildings. 

**What is the top 10 longest average dispatch response to an incident?**
![visual04](https://github.com/stephchen0816/NYC-Fire-Incident-Dispatch-Data-Analysis/assets/144307777/91c98a68-6686-4cd8-8f95-93d014b59176)
The graph above visualizes is the top 10 highest average dispatch response seconds per incident type. This shows on average how long each incident takes to respond. Based on this graph, it takes incidents regarding alarm systems the longest to respond on average. This graph is unsurprising as these incidents do not seem as important as other incidents mentioned in earlier visualization. This data however, should be taken into consideration in how to avoid these types of incidents so we can use the resources for other dire incidents instead. 
