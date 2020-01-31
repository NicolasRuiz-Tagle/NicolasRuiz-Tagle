# NCUA5300CallReport_ETL
Extracts the data from the zip files provided by the NCUA 5300 Call Report and imports the data to a database.


NOTE: Althought each zip file only contains about 5000 rows of data, there are hundreds of columns provided in any given csv file. This causes the code to run relatively slow and since we will be using a SQlAlchemy engine, all fields will default to varchar() in the SQLite database once it is exported. This becomes irrelevant because the data will then be exported to PowerBI where we can update each column to our desired column types of integers/floats wherever necessary. Also, I found that trying to update each column once it is imported to the SQLite database causes the database to blow up because the row size has limitations and apparently having all columns converted to integers causes each row to exceed the maximum allowed row size. This was true for MS SQL Server and the SQLite database, however, I am yet to test in Oracle or MySQL databases.


Requirements
1) Anaconda - We will be using Jupyter Notebooks and the code will be written in Python.
2) SQL Database - We will be using SQLite for this particular ETL, but the code can be updated for use in Oracle, SQL Server, or MySQL if necessary/
3) Power BI

Objective: To extract all of the data that is provided to the general public by the NCUA governing body. The NCUA 5300 Call Report contains the public information that all credit unions must report to the NCUA governing body. This data will be used to export to Power BI for additional visualizations and analytics. Please make note that the code will be written for uploading to a SQLite database, so be wary of changes in SQL syntax if updating for MS SQL Server or Oracle databases.


Procedure:
1) Navigate to the NCUA website containing the zip files. Website can be found here: 
https://www.ncua.gov/analysis/credit-union-corporate-call-report-data/quarterly-data

2) Download the desired zip file that you will be extracting. Begin with the most updated quarterly report due to the fact that we will be using SQLAlchemy to export the data and we want to create all the columns found in the most recent file. The older zip files may not contain all of the columns, so by using the most recent file when beginning this process, you are ensuring that you SQLAlchemy engine creates a new table with the most columns possible. 
NOTE: At most one zip file can be worked on at any given time. The code does not support unzipping multiple zip files unless manipulated to do so.

3) Place the zip file in the "Place Zip File Here" folder that is created within this repository.

4) Open the Jupyter notebook containing the master code. 

5) Run all cells - NOTE: this process is time consuming and can take anywhere between 15-20 minutes so feel free to grab a cup of coffee while you wait for the code to execute.

6) Open the SQLite database browser and query the database with the reporting period of the zip file you have uploaded. Ensure that the number of records in the database (number of rows) matches the row count within the zip files extracted.

7) Copy/Past the SQL query that is saved under the "SQL" folder to begin the data exporting process to PowerBI.

8) Connect to your SQLite database in PowerBI, use import data, and paste the SQL Query which will extract only the contents to be used in the Power BI Report. NOTE: you can call additional fields if necessary, I've only extracted those that I found of most importance. 

