# nosql-challenge

## Table of Contents
- [About](#about)
- [Key Steps](#key-steps)
   - [Database and Jupyter Notebook Set Up](#database-and-jupyter-notebook-set-up)
   - [Database Updates](#database-updates)
   - [Exploratory Analysis](#exploratory-analysis)

## About
In this project I evaluated the hygiene ratings of various food establishments across the U.K.
The ratings were provided by the UK Food Standards Agency. I provided the results of my evaluation to the food magazine, 
*Eat Safe, Love* , to help their journalists and food critics decide where to focus future articles.

## Key Steps
## **Database and Jupyter Notebook Set Up**
Imported establishments.json using `mongoimport`.
Created an instance of the Mongo Client.
Verified uk_database and establishments collection were imported. <br>
## **Database Updates**
Performed CRUD operations using PyMongo.
         
## **Exploratory Analysis**
I addressed the following inquiries during the exploratory analysis:

1. Identified establishments with a hygiene score of 20.
2. Identified establishments in London with a RatingValue greater than or equal to 4, utilizing `regex` to search for London.
3. Determined the top 5 establishments with a RatingValue of 5, sorted by the lowest hygiene score, with priority given to those closest to the "Penang Flavours" restaurant.
4. Calculated the number of establishments in each Local Authority area that have a hygiene score of 0, and presented the results in descending order, listing the top ten local authority areas. This was achieved using `aggregation` methods.

