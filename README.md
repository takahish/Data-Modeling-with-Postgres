# Data Modeling with Postgres

## Required libraries

- pandas
- psycopg2
- sql_queries

## Motivation

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

## Specification

Created tables must be normalized and stored into PostgreSQL. In addtition for analyzing user activity, Fact and Dimension tables must be created from songs metadata and log files.

## Files

- etl.ipynb: this notebook to develop the ETL process for each tables
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
<img src="assets/songplays.png" height="240">

### Dimension Tables

#### users - users in the app
- user_id, first_name, last_name, gender, level
<img src="assets/users.png" height="170">

#### songs - songs in music database
- song_id, title, artist_id, year, duration
<img src="assets/songs.png" height="170">

#### artists - artists in music database
- artist_id, name, location, lattitude, longitude
<img src="assets/artists.png" height="180">

#### time - timestamps of records in songplays broken down into specific units
- start_time, hour, day, week, month, year, weekday
<img src="assets/time.png" height="180">

## Acknowledgements

I wish to thank Udacity for advice and review.
