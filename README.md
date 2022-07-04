# NYC Yellow Taxi ETL pipeline project

This is an ETL pipeline to ingest NYC Yellow Taxi Records located [here](https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page). The file is ingested, transformed and loaded to our data warehouse. The data pipeline is built using Google Cloud Storage (GCS), Google Big Query. We use Spark as data transformation and Airflow as the orchestration. 

## Architecture diagram

![Draw2](https://user-images.githubusercontent.com/107358349/177057567-3fc223c3-a3ad-4e11-a614-c78d6d39787b.png)

## How it works

#### Overview

- Airflow is reponsible for the execution of the data ingestion to GCP. It is run in our Docker container.
- Google Cloud Platform (GCP) infrastructure is provisioned by Terraform. Once we run the config files using  ```terraform apply``` command, it creates the Big Query (data warehouse) and GCS (data lake) in GCP.


#### ETL pipeline

ETL flow consists two parts: Ingestion and Transformation.

In the first pipeline, Airflow manages and executes these following tasks:

![image](https://user-images.githubusercontent.com/107358349/177059033-297fb5e8-ca40-4bff-b4ef-539e2e2bf91d.png)

- Data is downloaded in CSV format. 
- Create a function to replace the file to Parquet format.
- Upload data to GCS.
- Transfer data to Big Query.

In the second pipeline, we transform the data using Spark then load it back to the Big Query. Transformations perfomed include modifying column name, joining taxi zone  table to our data, splitting datetime column, and aggregating functions.

## How to run the project

#### Prerequisites
