## Zillow-Data-Analytics-Rapid-API-End-To-End-ETL-Pipeline-Project

## Overview

The Zillow Data Analytics Project extracts housing data from Zillow using the Rapid API, processes it, and visualizes it using Amazon Web Services (AWS) services. The project utilizes Python, AWS EC2, Airflow, S3, Lambda, Redshift, and Quicksight for data extraction, transformation, and visualization.

## Architecture

**Data Extraction:** Python scripts are used to extract data from Zillow via the Rapid API. The extracted data is stored in an S3 bucket, which serves as the Landing Zone.

**Data Transformation:** AWS Lambda function is triggered by the arrival of extracted data in the Landing Zone. This function copy the data and load it into another S3 bucket, which acts as the Intermediate Zone.

**Data Loading:** Another Lambda function is triggered when data is copied into the Intermediate Zone. This function further transforms the data by doing necessary transfromations and loads it into a third S3 bucket, here the transformed data is stored.

**Data Orchestration:** Apache Airflow is used to orchestrate the entire workflow. It monitors the S3 bucket for the presence of transformed data and triggers the next steps in the process.

**Data Loading into Redshift:** Once the data is transformed and stored in the final S3 bucket, Airflow triggers the loading of this data into an Amazon Redshift data warehouse using the **S3ToRedshiftOperator.**

**Data Visualization**: Amazon QuickSight is connected to the Amazon Redshift cluster to visualize the Zillow data.

## Project Structure

The project is structured as follows:

**Python Scripts:** Contains scripts for data extraction from Zillow using the Rapid API.

**Airflow DAG:** Defines the workflow using Apache Airflow. It includes tasks for data extraction, transformation, loading into S3, and loading into Redshift.

**Configuration Files:** Includes the JSON configuration file for API keys and other settings.

## Installation and Setup

**AWS Setup:** Set up an AWS account and configure EC2, S3, Lambda, Redshift, and QuickSight.

**Rapid API:** Obtain API keys from the Rapid API website for accessing Zillow data.

**Airflow Setup:** Set up Airflow on an EC2 instance and configure it to run the DAG.

**Execution:** Trigger the Airflow DAG to start the data extraction from Zillow using Rapid API, transfromation and loading into Redshift Data Warehouse.

## Usage

**Data Extraction:** Run the Python scripts to extract data from Zillow and store it in the Landing Zone S3 bucket.

**Data Transformation** The Lambda function automatically copies the data into the Intermediate Zone S3 bucket.

**Data Loading:** Another Lambda function further transforms the data and loads it into the final S3 bucket.

**Data Loading into Redshift:** Airflow monitors the final S3 bucket and triggers the loading of data into Redshift using the S3ToRedshiftOperator.

**Data Visualization:** Connect Amazon QuickSight to the Redshift cluster to visualize the Zillow data.

