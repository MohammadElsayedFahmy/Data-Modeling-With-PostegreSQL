# Project 1: Data Modeling with Postgres


## Introduction 

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.


## Problem Statment

In this project, you'll apply what you've learned on data modeling with Postgres and build an ETL pipeline using Python. To complete the project, you will need to define fact and dimension tables for a star schema for a particular analytic focus, and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.



## Song Dataset

The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are file paths to two files in this dataset.

* song_data/A/B/C/TRABCEI128F424C983.json
* song_data/A/A/B/TRAABJL12903CDCF1A.json

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

* {"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}

## Log Dataset
The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate activity logs from a music streaming app based on specified configurations.

The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset.
* log_data/2018/11/2018-11-12-events.json
* log_data/2018/11/2018-11-13-events.json


## Running the Python Scripts
In Jupyter Notebook

1. ```%run create_tables.py```
2. ```%run etl.py```

## Database Schema

After examining the Log and Song JSON files, I created a Star schema  that include one Fact table (songplays) and 4 Dimension tables.

Schema for Song Play Analysis using the song and log datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables.This design will offer flexibility with the queries being used for analysis.

### Fact Table
songplays - records in log data associated with song plays i.e. records with page NextSong
songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
### Dimension Tables
1- users - users in the app 
* user_id, first_name, last_name, gender, level
2- songs - songs in music database
*song_id, title, artist_id, year, duration
3- artists - artists in music database
* artist_id, name, location, latitude, longitude
5- time - timestamps of records in songplays broken down into specific units
* start_time, hour, day, week, month, year, weekday

## Description of Files

### data/log_data

This directory contains a collection of JSON log files. These files are used to complete our Fact table  and also to complete the dimensions tables.

### data/song_data

This directory contains a collection of Song JSON files. These files are used to Complete  Dimension tables for Songs and Artists.

## create_tables.py

The python script creates the database and the tables where the data is stored.

## etl.ipynb

A Python Jupyter Notbook that was used for data exploration and testing of the ETL process..

## etl.py

This Python script reads into the Log and Song data files, handles and inserts the data into the database.

## sql_queries.py

A Python script which defines all the SQL statements used in this project.
## test.ipynb

A Python Jupyter notebook that was used to test that the data was loaded correctly.