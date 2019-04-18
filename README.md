# Data Modeling with Postgres

## Required libraries

- pandas
- psycopg2
- sql_queries

## Motivation

I learn Data Modeling with RDM by using JSON metadata that represents the songs and JSON files that represents user activity.

## Project

Created tables must be normalized and stored into PostgreSQL. In addtition for analyzing user activity, Fact and Dimension tables must be created from songs metadata and user activity logs.

## Files

- etl.ipynb: this notebook to develop the ETL process for each tables
- test.ipynb: this notebook to test sql_queries.py and elt.ipynb (etl.py) 
- create_tables.py: create database and tables
- elt.py: define the ETL process
- sql_queries.py: define the SQL queries

## Data

### Songs metadata

The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

```
song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json
```

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

```
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}
```

### User activity logs

The log files in the dataset you'll be working with are partitioned by year and month. For example, here are filepaths to two files in this dataset.

```
log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json
```

And below is an example of what a single activity log in 2018-11-13-events.json, looks like.

```
{"artist":null,"auth":"Logged In","firstName":"Kevin","gender":"M","itemInSession":0,"lastName":"Arellano","length":null,"level":"free","location":"Harrisburg-Carlisle, PA","method":"GET","page":"Home","registration":1540006905796.0,"sessionId":514,"song":null,"status":200,"ts":1542069417796,"userAgent":"\"Mozilla\/5.0 (Macintosh; Intel Mac OS X 10_9_4) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/36.0.1985.125 Safari\/537.36\"","userId":"66"}
```

## ETL Processes

The summary of ETL processes is below.
For more details, see etl.ipynb, etl.py and sql_queries.py.

### Songs metadata

#### #1: songs table

- Parse and read a song JSON file by using pandas.read_json function.
- Select columns for song ID, title, artist ID, year, and duration from dataframe.
- Execute an insert query to songs table in PostgreSQL.
  - If the song ID confliction is occured, do nothing.
- Repeat the process iterably for all songs data.

#### #2: artists table

- Parse and read a song JSON file by using pandas.read_json function.
- Select columns for artist ID, name, location, latitude, and longitude from dataframe.
- Execute an insert query to artists table in PostgreSQL.
  - If the artist ID confliction is occured, do nothing.
- Repeat the process iterably for all songs data.

### User activity logs

#### #3: time table

- Parse and read a JSON file of user activity log by using pandas.read_json function.
- Filter records by NextSong action.
- Convert the ts timestamp column to datetime.
- Extract the timestamp, hour, day, week of year, month, year, and weekday from dataframe.
- Execute an insert query to time table in PostgreSQL.
- Repeat the process iterably for all log files.

#### #4: users table

- Parse and read a JSON file of user activity log by using pandas.read_json function.
- Filter records by NextSong action.
- Select columns for user ID, first name, last name, gender and level from dataframe.
- Execute an insert query to songs table in PostgreSQL.
  - If the user ID confliction is occured, Update value of level on the recored.
- Repeat the process iterably for all log files.

#### #4: songsplays table

- Parse and read a JSON file of user activity log by using pandas.read_json function.
- Filter records by NextSong action.
- Select the timestamp, user ID, level, song ID, artist ID, session ID, location, and user agent from dataframe.
  - Log files don't include song ID and artist ID, so get these ID by executing select query to songs and artists tables.
- Execute an insert query to songs table in PostgreSQL.
- Repeat the process iterably for all log files.

## Usage

Create tables and execute ETL.

```
$ python create_tables.py
$ python etl.py
```

## Result tables

### Fact Table

#### songplays - records in log data associated with song plays.
- table description
<img src="assets/desc_songplays.png" height="250">

- examples
<img src="assets/songplays.png" height="250">

### Dimension Tables

#### users - users in the app
- table description
<img src="assets/desc_users.png" height="170">

- examples
<img src="assets/users.png" height="170">

#### songs - songs in music database
- table description
<img src="assets/desc_songs.png" height="170">

- examples
<img src="assets/songs.png" height="170">

#### artists - artists in music database
- table description
<img src="assets/desc_artists.png" height="170">

- examples
<img src="assets/artists.png" height="180">

#### time - timestamps of records in songplays broken down into specific units
- table description
<img src="assets/desc_time.png" height="200">

- examples
<img src="assets/time.png" height="180">

## Acknowledgements

I wish to thank Udacity for advice and review.
