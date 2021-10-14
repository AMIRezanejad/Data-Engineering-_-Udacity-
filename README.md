# Postgres ETl on Sparkify dataset
 
 In the first Project of Nano Degree ,the following task will be executed:
 - data modeling with postgres 
 - Datawarehouse Star Schema  
 - ETL pipeline with Python

# Overview
 
 Sparkify is an open source music stream app which it has obviousely a database and ubstructure data round users and songs and all activity around interaction of Users and the JSON log files which shows user activity on the app anda metadata about songs and users.
 in this project we work out on the Database schema , building a cube and ETL pipeline for this Analysis.

# Data Resources

 the whole Data are stored  in the two main categories: Song Datasets and Log Datasets
 
 Song Datasets: all json files are nested in subdirectories under /data/song_data. A sample of   this files is:
 
 ```{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}```
 
 Log datasets: all json files are nested in subdirectories under /data/log_data. A sample of a single row of each files is:
 
```{"artist":"Slipknot","auth":"Logged In","firstName":"Aiden","gender":"M","itemInSession":0,"lastName":"Ramirez","length":192.57424,"level":"paid","location":"New York-Newark-Jersey City, NY-NJ-PA","method":"PUT","page":"NextSong","registration":1540283578796.0,"sessionId":19,"song":"Opium Of The People (Album Version)","status":200,"ts":1541639510796,"userAgent":"\"Mozilla\/5.0 (Windows NT 6.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/36.0.1985.143 Safari\/537.36\"","userId":"20"}```

# Database Schema for Song Play Analysis

The Star Schema is executed in this exercise. the schema included one fact table which is named songplays and four dimentioal tables with primary keys in each table that are referenced from the fact tables.


#### Fact Table
##### songplays - records in log data associated with song plays 
- songplay_id (INT) PRIMARY KEY: ID of each user song play
- start_time (DATE) NOT NULL: Timestamp of beggining of user activity
- user_id (INT) NOT NULL: ID of user
- level (TEXT): User level {free | paid}
- song_id (TEXT) NOT NULL: ID of Song played
- artist_id (TEXT) NOT NULL: ID of Artist of the song played
- session_id (INT): ID of the user Session
- location (TEXT): User location
- user_agent (TEXT): Agent used by user 

#### Dimension Tables

**users**- users in the app
- user_id (INT) PRIMARY KEY: ID of user
- first_name (TEXT) NOT NULL: Name of user
- last_name (TEXT) NOT NULL: Last Name of user
- gender (TEXT): Gender of user {M | F}
- level (TEXT): User level {free | paid}

**songs** - songs in music database
- song_id (TEXT) PRIMARY KEY: ID of Song
- title (TEXT) NOT NULL: Title of Song
- artist_id (TEXT) NOT NULL: ID of song Artist
- year (INT): Year of song release
- duration (FLOAT) NOT NULL: Song duration in milliseconds

**artists** - artists in music database
- artist_id (TEXT) PRIMARY KEY: ID of Artist
- name (TEXT) NOT NULL: Name of Artist
- location (TEXT): the city that artist located
- lattitude (FLOAT): Lattitude location of artist
- longitude (FLOAT): Longitude location of artist

**time**- timestamps of records in songplays broken down into specific units
- start_time (DATE) PRIMARY KEY: Timestamp of row
- hour (INT): Hour involved with start_time
- day (INT): Day involved  with  start_time
- week (INT): Week of year involved  with start_time
- month (INT): Month involved  with start_time
- year (INT): Year involved  with start_time
- weekday (TEXT): Name of week day involved  with start_time


# Project Workflow
 
 the foloing steps will execute truely the process of ETL:
 - write the all the queries which we need in the ETL pipeline including (DDl,DML Queries) and they are collected  in `sql_queries.py`.
 - execute the python program to execute DDL queries means creating our database and Data warehouse with the Queries which we have written in the first step. the execution file named by `create_tables.py`.
 - read and process and testing the reading a single file from the data resources and load the data into the Tables that are already built.actually we feed the table and we test the following ETL workflow works well or not.the whole process of ETL will execute in the `etl.ipynb` jupiter notebook.
 - implement the reading the whole data from data sources which are already tested in the Jupiter notebook.the process is written and implemented in `etl.py` file.
 - the whole process of the ETL can be test base on implementing the queries which are collected in the `test.ipynb`.
  
 # The Project Execution 
 
- Write DROP, CREATE , INSERT and SELECT queries  in ```sql_queries.py```

- Run it in console ```python create_tables.py```
- implement ```test.ipynb``` Jupyter Notebook to test that all tables were created correctly.
- complete the whole ETL process pathway in etl.ipynb Notebook to create the  pipeline to process and insert a sample data into the tables.
- Test again the the Sample Pipeline will run correctly in ```test.ipynb```, filled in etl.py program.
- Run etl in console, achieve the Result of final ETL Process: ```python etl.py```
