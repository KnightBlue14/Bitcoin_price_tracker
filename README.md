# Bitcoin_price_tracker
A Capstone project testing the use of APIs, as well as other Data Engineering skills

## Description
This is a personal project developed as a test of my abilities after time on a Data Engineering course, combining API data extraction, transformation for uplaoding to a SQL databases, and loading to and from said database directly from a python instance. The goal was to create an application that could pull the price of Bitcoin in multiple currencies 
from the 'Coindesk' API, generate an initial block of data, then run automatically to download and append the recent figures, with a utility for visualisation. These three stages have been separated into individual files, allowing for each to be run without any unwanted additional changes.

## Technologies used
* Python - this project is primarily written in python, with some SQL for uploading data to the 'pagilla' database with the 'psycopg2' module. While the credentials in the script are no longer valid, they were only needed for accessing the database, and could easily be changed to a locally hosted instance, such as a MySQL database.
* SQL - The data pulled from the API was sent to a 'pagilla' database for long-term storage, and uses some basic SQL commands, though knowledge of SQL commands is not essential for using this application, since it can also pull data for visualisation in python.
* Coindesk - The bitcoin price figures are pulled from Coindesk, an online crypto media hub. They provide news for a wide variety of crypto-related topics, including market conditions, technology and current events. https://www.coindesk.com/

## Script blocks
### Capstone Project - Master.ipynb
This is the master version of the project, combining all of the other blocks into one, and is also 'dirtier' compared to the others. Each of the blocks will be covered in their own sections.

### Capstone Project - Test data.ipynb
This script is for generating an inital block of data for testing purposes, and will output to the 'datablock' database. Due to unknown reasons, while the script does function, it only provides figures up to 2022, at the time of writing, leaving a year long gap between this data and the data gathered in the Update portion of this project, hence why they
are stored in seperate databases.
The script gathers the data from the Coindesk API, currency by currency. In the script, it is currently set to use 5 currencies, though it can go as high as 150. This figure was cut down for testing, as gathering all of them results in several minutes of runtime. It initially uses timestamps to build an initial dataframe, then appends the currency data,
ensuring that all of the data is appropriately ordered. From there, it is pushed to the SQL database for storage.

### Capstone Project - Update.ipynb
Similar to the Test Data block, this script gathers Bitcoin prices from Coindesk, though this one uses the current figures (at time of runnning) rather than a block of historical data. It then performs a small transformation for compatability, and pushes it to the 'databrick' database, separate from the test data for the reasons mentioned above. This script 
is built with the intention to run it repeatedly, appending to the database with each use.

### Capstone Project - Visualise.ipynb
The finla script is for visualisation of the data gathered in the other parts. It is divided into two blocks, one for each database. The 'datablock' figure represents the test data, covering three years of data, resulting in a graph clearly showing the trends in price over time, in USD. The 'databrick' figure covers the more recnt data, which, as mentioned, 
had a large gap between it and the test data, meaning it only started growing once it was built, resulting in a much shorter graph. Both also have a user function, allowing them to choose which currency is displayed, limited to 5 for testing purposes. The user must enter the uncapitalised currency code to display the data. If the user does not know the code, 
they can instead type 'code' for a list of available currencies.

## Issues
While the project overall does function, there are issues that limit it's functionality.
* As stated earlier, the historical data cuts out a at a year prior to the user date, resulting in a gap between the test data and current data. Due to this, the user would need to run the script for some time before it could be used to observe any trends, and even then it would not relate to any prior trends.
* In it's current state, the script will only gather 5 languages. This is a simple fix, as the required code is commented out, but the visualisation portion would need to be updated to include the additional currencies. (Note - during testing, it was found that including the 'BTC' currency would result in an error. This should be excluded anyway, as it would
provide the Bitcoin price in the Bitcoin currency. That is, 1)
* The authentication details provided are no longer valid, and need to be changed to a valid SQL database.
