# Sparkify Project:  Data Modeling with *Postgres*
This is a database project for a music streaming startup Sparkify.  Sparkify is looking to perform analytics on suscribers and the songs they are listening to.  The raw data that Sparkify has is in two parts.  The first is the list of songs that are available for listening to users.  The second is a log of user activity on the app -- what songs they have listened to, and when.  Both parts are in *JSON* format.

## ETL Process
The data directory contains the raw data in *JSON* format that is processed.  The *song_data* folder contains the files with information on each song available for listening (one song per file), with metadata about a song and the artist for that song.  The *log_data* folder contains the files with information on listening sessions (one session per file), with metadata about the user, song listened to, and time spent listening.

The data from the song and log files are extracted with the help of the *pandas* library in *Python*.  The files are stored in a Python dataframe and, where necessary, transformed into appropriate formats to be loaded into the SQL tables.  For example, a column stored as a timestamp is converted to datetime format, which works better for the SQl tables.

## Database Design and Schema
Using the song and log datasets, a star schema is used and optimized for queries on song play analysis.  This includes the following tables:
### Fact Table
1.  **songplays** - records in log data associated with song plays 
    - *songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

### Dimension Tables
2.  **users** - users in the app
    - *user_id, first_name, last_name, gender, level*
3.  **songs** - songs in music database
    - *song_id, title, artist_id, year, duration*
4.  **artists** - artists in music database
    - *artist_id, name, location, latitude, longitude*
5.  **time** - timestamps of records in **songplays** broken down into specific units
    - *start_time, hour, day, week, month, year, weekday*

## Project Repository Files
*   *song_data* and *log_data* - contains the raw song data and listening logs in *JSON* format
*   *sql_queries.py* - contains the table creation, insert statements, and a query to search for a song
*   *create_tables.py* - creates the database and executes statements in 
*sql_queries.py*
*   *etl.py* - the main program, processes the data files to load the database

### Running the program
To run this project, download the project files and run `python create_tables.py`, which will execute *sql_queries.py*.  Then, run `python etl.py` to perform the etl process.  Running `python test.ipynb` will show some of the data entered in the tables.