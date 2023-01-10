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

## ETL Pipeline

This script is responsible for processing the data files in json format and loading them into the Sparkify database. The data includes song information and event logs, which is extracted and transformed into a format suitable for loading into a Postgres database. The script uses the following libraries:
* os: To access the filesystem and search for json files
* glob: To search for json files
* psycopg2: To connect to and interact with the Postgres database
* pandas: To read and manipulate the json data
* sql_queries: A module containing the SQL statements for inserting data into the tables

### Functionality

The script defines three main functions:
1. `process_song_file(cur, filepath)`: Given a cursor and filepath, this function will read the song file in json format and insert the data into the songs and artists table
2. `process_log_file(cur, filepath)`: Given a cursor and filepath, this function will read the log file in json format and insert the data into the time, users and songplays table
3. `process_data(cur, conn, filepath, func)`: Driver function that calls the above two functions on all json files found in the filepath directory.

### Usage

The script should be run with the command python etl.py. Before running the script, it is important to ensure that the correct file path is provided and that the database details are correct in the script. The script will start by searching for all json files in the specified filepath, and then it will process the song and log files separately, inserting the data into the songs, artists, time, users and songplays tables.

It is important to note that, the script will only search for json files in the specified filepath directory, so it is important to make sure that the correct data files are located in the specified directory.

After the data is loaded, the script will print the number of records inserted for each file processed. This will help in tracking the progress of the script.

It is also important to note that running this script will insert data into the database, so if you wish to start fresh, you should drop and create the database tables before running this script.

Once the script completes, you can run analytical queries to extract insights and make business decisions using the data in the database.
