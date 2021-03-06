# Surfs Up! - An SQLAlchemy Project

## Background
In this project, I tasked myself with climate analysis of Hawaii by using advanced data storage and retrieval using SQLAlchemy ORM queries, Pandas, and Matplotlib

**NOTE**: The [sqlite database](https://github.com/jaryan77/sqlalchemy-challenge/blob/main/Resources/hawaii.sqlite) for this project was already provided.
#
## Climate Analysis and Exploration

* Using SQLAlchemy `create_engine`, I connected to my sqlite database
* Next, I used `automap_base()` to reflect my tables into classes and saved a reference to those classes called `Station` and `Measurement`.
* Finally, link Python to the database by creating an SQLAlchemy session.

![create_classes.png](Images/create_classes.PNG)

### Precipitation Analysis
* By finding the most recent date in the data set, I retrieved the last 12 months of precipitation data by querying the 12 preceding motnhs of data. 
    * I was careful not to pass in the date as a variable to my query.

* Next, I selected `date` and `prcp` values, loaded the query results into Pandas DataFrame and set the index to the date column, and sort the DataFrame values by `date`.
* Next, I plotted the results using the DataFrame `plot` method.

![precip_plot.png](Images/precip_plot.PNG)

* I also used Pandas to print the summary statistics for the precipitation data.

![summary_stats.png](Images/summary_stats.PNG)

### Station Analysis

* To start of my station analysis, I designed a query to calculate the total number of stations in the dataset.

* Next, I sought out the most **active** stations i.e. the stations that have the most rows in the dataset. 
* I then completed the following queries using `func.min`, `func.max`, `func.avg`, and `func.count`:
    * List the stations and observation counts in descending order.
    * Which station id has the highest number of observations?
    * Using the most active station id, calculate the lowest, highest, and average temperature.

* I then designed a query to retrieve the last 12 months of temperature observation data (TOBS).
* To complete this task, I completed the following steps:
    * Filter by station with the highest number of observations.
    * Query the last 12 months of temperature observation data for this station.
    * Plot the results as a histogram with `bins=12`

![histogram.png](Images/histogram.PNG)

### Close Section
* As this is the completion of my climate analysis, I was sure to close this session using `session.close()` before moving on to my climate app
#

## Climate App

Now that I have finished my climate analysis, I went on to design a Flask API based on the queries that I have developed.

### Using Flask, I created the following routes:

* `/`
    * This is the Home Page that lists all routes available

* `/api/v1.0/stations`
    * This route returns a JSON representation of my dictionary

* `/api/v1.0/tobs`
    * This route returns a JSON list of TOBS for the previous year

* `/api/v1.0/<start>` and `/api/v1.0/<start>/<end>`
    * This route returns a JSON list of the minimum temperature, the average temperature, and the maximum temperature for the given start or start-end range.
