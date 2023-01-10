# Sparkify ETL Pipeline

This repository contains the ETL pipeline for populating the Sparkify database, which is designed to enable Sparkify to analyze data on its users, the songs they listen to, and the artists of those songs. The database provides a consistent and reliable source to store this data, which will be useful in helping Sparkify reach some of its analytical goals, such as finding the most popular songs or identifying high-traffic times of the day.

## Database Design

<center><img width="354" alt="schema" src="https://user-images.githubusercontent.com/47195793/211654606-65a33bca-bf9c-4a04-8aa3-a88a31b7abc9.png"></center>
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

## Database Creation and Table Management

This script is responsible for creating a database called sparkifydb and managing the tables within it. It uses the psycopg2 library to connect to a Postgres database, and the sql_queries module which contains the SQL statements for creating and dropping the tables.

### Functionality

The script provides three main functions:
1. `create_database()`: This function connects to the Postgres server and creates the sparkifydb database with UTF8 encoding and sets autocommit as True. It returns the cursor and connection references which can be used to run other database queries.
2. `drop_tables(cur, conn)`: Given a cursor and a connection, this function will run all the DROP TABLE queries in the sql_queries module.
3. `create_tables(cur, conn)`: Given a cursor and a connection, this function will run all the CREATE TABLE queries in the sql_queries module.

### Usage

The main() function calls the `create_database()`, `drop_tables()`, and `create_tables()` functions in that order. It is expected that the database does not exist at the time of running this script, but if it does then it will be dropped first. 

After the tables are created, the function will close the database connection.

It is important to ensure that the connection details like host,user,password etc are correct in the script.

You can run this script by running the command `python create_tables.py` in the command line.

The database is intended to be used for Sparkify's ETL pipeline, and the tables are designed to store data on users, songs, artists, and songplays.

It is very important to ensure that the correct details are given to the script. And this script should be used only once when the database is being set up.
