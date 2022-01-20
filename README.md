# Movies-ETL
Project focused on ETL - Extract, Load and Transform

## Overview
Amazing Prime Video (APV) is a platform for streaming movies and TV shows on Amazing Prime - the world's largest online retailer.
APV wants to develop an algorithm to predict which low-budget movies being released will be popular so they can make good deals in buying the streaming rights. In order to achieve that, APV will sponsor a hackaton which will provide a clean dataset of movie data and ask participants to predict popular movies.

Britta, an APV employee, has been tasked to create the dataset for the hackaton. She is in charge of creating a pipeline to import raw data from Wikipedia and MovieLens, clean it up and merge it into a single point to finally load the transformed data into a SQL Database.

## Data from Wikipedia
Wikipedia data is available in JSON format, which means more flexible format and non tabular data. For each movie entry, there can be an enormous variety of attributes and many of those can be similar. At a first glance, the dataset is intimidating because the import of raw data yields a table of 193 columns. With a lot of work and especially common sense, the data gets cleaned little by little. The steps taken to clean the data are described below.

- *Load raw data into a pandas datafrane and make first inspection(193 columns)* 
- *Identify if the entry refers to a movie or TV show (there must be a IMDB link for movies) and remove the ones that are NOT movies*
- *Identify all different attributes used to store a movie name (usually related to its native language - but not only) and consolidate them all into a single attribute (Also known as)*
- *Identify columns that hold the same information and consolidate them (for instance, 'Directed by' and 'Director')*
- *Create meaningful columns depending on the context (extract imdb from url and create a column just for that code)*
- *Identify patterns (like regular expressions) in order to fix date and numerical data*
- *Convert datatypes*

### Techniques used to clean JSON
- *Use of list comprehensions in Python to clean JSON data (and still have JSON format)*
- *Use of functions to go over entries fixing them*
- *Dictionary manipulation to consolidate attributes*
- *Consolidate columns by making merges*
- *Create new column(s)*
- *Use of regex to fix dates and numbers*
- *Remove mostly null columns*

## Data from MovieLens
- *Load raw data into a dataframe*
- *Inspect the columns to see if all the information is pertinent*
- *Inspect data and remove bad data*
- *Convert data to correct datatypes*

## Merge (Wikipedia and MovieLens) data
The merge process is another set of decision-making steps. Since there were two sources of data, the main idea here was to spot what data was best and decide which one to keep. The merge was made on IMDB column, the columns were paired up, and, for each column of interest, the following would apply:
- Inspect data and verify which source was best;
- Based on the first step, decide if a given column should be kept as is/dropped or if the final column would be a combination of the two (in such case, we need to choose which column would be the primary, and which would fill the blanks in case the first one was empty for a given entry)
It is especially important to emphasize that data can be dropped in this step as well. Data that shows to be inconsistent (for instance, basic data like movie name will not match) should be dropped.

## Results
The merge was satisfactory. We were able not only to clean the data in both initial datasets, but also to merge it without any big loss.

## *A word on ETL*
The ETL process followed to clean data is somewhat empirical. It is really a step at a time, you inspect the data, make a fix (and that can mean transforming data in a few or all rows/columns, eliminating data in a few/all rows/columns, etc) and then back to square one: you inspect what you have from the previous transformation and decide what to tackle next. Repeat and repeat till you inspect the data and consider it good enough for your purpose. 
More importantly, there is no exact recipe even on how to start because it all depends on the format of the data. ETL needs a lot of common sense, some good thought on how to deal with each transformation and occasionally a good deal of programming to make it happen. Coming from SQL world, I learned that sometimes it is easier to transform data in a list or dictionary level than in a SQL table mainly because of the structure of incoming data.
