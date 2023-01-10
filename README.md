# Sparkify ETL Pipeline

This repository contains the ETL pipeline for populating the Sparkify database, which is designed to enable Sparkify to analyze data on its users, the songs they listen to, and the artists of those songs. The database provides a consistent and reliable source to store this data, which will be useful in helping Sparkify reach some of its analytical goals, such as finding the most popular songs or identifying high-traffic times of the day.

## Database Design

The STAR schema is used for the database design, as it simplifies queries and provides fast aggregations of data. The schema includes the following tables:

- **users**: contains information on Sparkify users
- **artists**: contains information on songs and artists
- **time**: contains information on the timestamps of user sessions
- **songplays**: contains information on the songs played in each user session

## ETL Pipeline

Python is used for the ETL pipeline, as it contains libraries such as pandas that simplify data manipulation. The pipeline also uses the psycopg2 library to connect to the Postgres database.

There are two types of data involved in the pipeline:song data and log data. 
- Song data contains information about songs and artists, which is extracted from and loaded into the users and artists dimension tables.
- Log data gives information about each user session, and it is extracted and loaded into the time, users dimension tables and songplays fact table.

## Running the ETL Pipeline

1. Run `create_tables.py` to create the data tables using the specified schema design. If tables were previously created, they will be dropped and recreated.
2. Run `etl.py` to populate the data tables with the extracted data.

Note: Ensure that you have the correct database and connection details before running the scripts.
