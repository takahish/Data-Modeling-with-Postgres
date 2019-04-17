# Data Modeling with Postgres

## Required libraries

- pandas
- psycopg2
- sql_queries

## Motivation

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. Your role is to create a database schema and ETL pipeline for this analysis. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

## Files

- etl.ipynb: this notebook to develop the ETL process for each of your tables
- test.ipynb: this notebook to test sql_queries.py and elt.ipynb (etl.py) 
- create_tables.py: create database and tables
- elt.py: define the ETL process
- sql_queries.py: define the SQL queries

## Usage

Create tables and execute ETL.

```
$ python create_tables.py
$ python etl.py
```

Created tables by the command are as folow,

### Fact Table

#### songplays - records in log data associated with song plays.
- songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
<img src="assets/songplays.png">

### Dimension Tables

#### users - users in the app
- user_id, first_name, last_name, gender, level
<img src="assets/users.png">

#### songs - songs in music database
- song_id, title, artist_id, year, duration
<img src="assets/songs.png">

#### artists - artists in music database
- artist_id, name, location, lattitude, longitude
<img src="assets/artists.png">

#### time - timestamps of records in songplays broken down into specific units
- start_time, hour, day, week, month, year, weekday
<img src="assets/time.png">

## Acknowledgements

I wish to thank Udacity for advice and review.
