# NYC Yellow Taxi ETL pipeline project

This is an ETL pipeline to ingest NYC Yellow Taxi Records located [here](https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page). The file is ingested, transformed and loaded to our data warehouse. The data pipeline is built using Google Cloud Platform (GCP) including Google Cloud Storage (GCS), Google Big Query, Spark as data transformation and Airflow as the orchestration. 

## Architecture diagram

## How it works

#### Overview

- GCP infrastructure is provisioned by Terraform. Once we run the config files using  ```terraform apply``` command, it creates the Big Query (data warehouse) and GCS (data lake) in GCP.
- Airflow is reponsible for the execution of the data ingestion to GCP. It is run in our Docker container.

#### ETL pipeline

Airflow has 4 tasks:

- In the first task, data is downloaded in CSV format. 
- In the second task, we create a function to replace the file to Parquet format.
- In the third task, data is uploaded to GCP storage bucket.
- In the fourth task, data is transferred to BigQuery.

#### Example runtime

## How to run the project

#### Prerequisites
