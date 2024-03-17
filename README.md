# Data_Analysis_BirdStrike_Incidents


## Overview
In this practicum you will build a database that can be used to analyze bird strikes on aircraft. For an existing data set from the FAA [1], you will build a logical data model, a relational schema, realize the relational schema in MySQL/MariaDB, load data into the database, execute SQL queries, a finally perform some simple analysis of the data.

The average time to complete the practicum is 15-25 hours. Do not wait to start. Seek help early. Submit often and as soon as you have enough code that works. We will only grade the last submission. Check your submission before you submit and after.

The graphic below shows some statistics regarding bird strikes and helps frame the data in the data file.

Bird Strikes In US 2000-2011.png  

Here is a report from CNN about a recent bird strike during a commercial flight from Atlanta, GA.

Use the provided time estimates for each tasks to time-box your time. Seek assistance if you spend more time than specified on a task -- you are likely not solving the problem correctly. A key objective is to learn how to look things up, how to navigate complex problems, and how to identify and resolve programming errors.

## Learning Objectives
In this practicum you will learn how to:

install/procure MySQL or MariaDB
connect to MySQL/MariaDB from R in an R Notebook
build a relational schema in at least 3NF (but ideally in BCNF) for an existing data set
load data from CSV files into a relational database through R
execute SQL queries against a MySQL/MariaDB database through R
perform simple analytics in R
identify and resolve programming errors
look up details for R, SQL, and MySQL/MariaDB
time-box work




## (20 pts / 2.5 hrs) Inspecting the data file; 

assume that this database will be used for an app that can be used by pilots (of any kind of aircraft) to report wildlife incidents. Create a new database and connect to it from R. 

Then create the following database schema:
Create a table that stores bird strike incident called incidents(iid, date, origin, airline, aircraft, flightPhase, impact, cond). Only store the date, not the time of the incident. Make 'impact' a Boolean flag and use TRUE if there was damage, FALSE otherwise. Use appropriate data types and store the date as a date type not as text subject to the data types your chosen database supports. If date or boolean are not supported, choose another data type that will work or split the dates into month, day, and year columns.

Create a table that stores airports and states called airports(aid, airportName, airportCode, state). The airport code should be the airports international code, e.g., BOS for Boston or LGA for LaGuardia. However, you may leave it empty for this database -- it is for future expansion.
Link the incidents and airports tables via the origin foreign key. 

Create a lookup table conditions(cid, condition, explanation) and link this lookup table to the incidents table with the cond foreign key. This table contains the value of all conditions, e.g., 'Overcast'. Leave the explanation column empty (future expansion).
Harmonize the flight phases to be one of: takeoff, landing, inflight, unknown. For example, for row 14, the flight phase was provided as "Landing Roll" -- change that to "landing" when storing the flightPhase. Code 'approach' as 'landing'; code 'climb' as 'takeoff', etc. Use your judgement as to what the appropriate harmonization is.

Assume "Business" to be an airline name.
Remove all military flights from the database.

You may either use {sql} code chunks or calls to R functions to execute the SQL statements. 
(25 pts / 5 hrs) Place the Bird Strikes CSV file into the same folder as your R Notebook and the load it into R without a path name. The default path is the local folder that contains the R Notebook when you have the R Notebook in an R Project. Once loaded, populate the tables with the following subset of data. Use the following column mappings:

FlightDate ---> incidents.date
Aircraft: Make/Model ---> incidents.aircraft
Effect: Indicated Damage ---> incidents.impact
Conditions: Sky ---> conditions.condition
When: Phase of flight ---> incidents.flightPhase
Airport: Name ---> airports.airport
Origin State ---> airports.state
Aircraft: Airline/Operator ---> incidents.airline

Use default values where the data file does not contain values or leave empty. Records (rows) from the CSV that do not have flight information may be omitted. If there is no airport or airline, then link to a "sentinel" airline or airport, i.e., add an "unknown" airline and airport to the tables rather than leaving the value NULL. Assign synthetic key values to aid, iid, and cid and use them as primary keys.
(5 pts / 1 hr) Show that the loading of the data worked by displaying parts of each table (do not show the entire tables).  Document and explain your decisions. See the Hints below for information on db4free. All data manipulation and importing work must occur in R. You may not modify the original data outside of R -- that would not be reproducible work. It may be helpful to create a subset of the data for development and testing as the full file is quite large and takes time to load.

(10 pts / 1 hr) Create a SQL query against your database to find the number of bird strike incidents for each flight phase. You may either use a {sql} code chunk or an R function to execute the query. It must be a single query.

(10 pts / 1 hr) Create a SQL query against your database to find the flight phase that had an above average number bird strike incidents (during any flight phase). You may either use a {sql} code chunk or an R function to execute the query. It must be a single query. 

(10 pts / 1 hr) Create a SQL query against your database to find the average number of bird strike incidents by month (across all years). Include all airlines and all flights. You may either use a {sql} code chunk or an R function to execute the query. It must be a single query.

(10 pts / 4 hrs) Build a column chart that visualizes the number of bird strikes incidents per year from 2005 to 2011. Adorn the graph with appropriate axis labels, titles, legend, data labels, etc.

(10 pts / 3 hrs) Create a stored procedure in MySQL (note that if you used SQLite, then you cannot complete this step) that adds a new bird strike incident to the database. You may decide what you need to pass to the stored procedure to add a bird strike incident and you must account for there being potentially a new airport. After insertion, show (in R) that your procedure worked. Note that if you used SQLite rather than the required MySQL for the practicum, then you cannot complete this question as SQLite does not support stored procedures.
Resources
[1] Data Visualization - Bird Strike Dataset by H. Haveliwala | data.worldLinks to an external site.
[2] R Markdown Cheat Sheet
[3] BirdStrikesData.csvDownload BirdStrikesData.csv
[4] PRIMER ON R
[5] LucidChart ERD & UML ToolLinks to an external site. 
[6] Using MySQL and MariaDB with R (jagg19.github.io)Links to an external site.
[7] RMariaDB: MariaDB Driver for R - MariaDB Knowledge BaseLinks to an external site.

