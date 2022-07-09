# NYC Yellow Taxi ETL pipeline project

This is an ETL pipeline to ingest NYC Yellow Taxi Records located [here](https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page). The file is ingested, transformed and loaded to our data warehouse. The data pipeline is built using Google Cloud Storage (GCS) and Google BigQuery. We use Spark as data transformation and Airflow as the pipeline orchestration for this project.

## Architecture diagram

![Untitled drawio (1)](https://user-images.githubusercontent.com/107358349/178117869-fc58808a-faeb-4f1d-9c86-06b2dc528331.png)


## How it works

#### Overview

- Airflow is responsible for the execution of the data ingestion to GCP. It is run in our Docker container.
- Google Cloud Platform (GCP) infrastructure is provisioned by Terraform. Once we run the configuration files using ```terraform apply``` command, it creates the BigQuery (data warehouse) and GCS (data lake) in GCP.


#### ETL pipeline

ETL flow consists of two parts: Ingestion and Transformation.

In the first pipeline, Airflow manages and executes the following tasks:

![image](https://user-images.githubusercontent.com/107358349/177059033-297fb5e8-ca40-4bff-b4ef-539e2e2bf91d.png)

- Download data from the website in CSV format. 
- Convert the file to Parquet format.
- Upload data to GCS.
- Create external table in BigQuery.

In the second pipeline, we transform the data using Spark in Jupyter Notebook and load it to BigQuery. Transformations performed include modifying column name, joining taxi zone table, splitting ```pep_pickup_datetime``` to year and month, and aggregating functions. We also add audited columns which are ```created_date``` and ```file_source```.

#### Final Result
![Yellow_Taxi_Trip_Records (2).pdf](https://github.com/fionangq/GCP-YellowTaxi-project/files/9050823/Yellow_Taxi_Trip_Records.2.pdf)



## How to run the project

#### Prerequisites
- Docker and Docker-Compose
- Python 3
- Google Cloud SDK
- Terraform
- Airflow locally
- GCP account: GCS and BigQuery
- Spark and Jupyter Notebook
