# Module 12: Nosql Challenge

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

## Tools
- PyMongo: Mongo Client
- Jupyter Notebook
- PANDAS

## Key Steps
#### **Database and Jupyter Notebook Set Up:**
Imported establishments.json and created an instance of the Mongo Client.
````
mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json
mongo = MongoClient(port=27017)
````
Verified uk_database and establishments collection were imported.

--------------------------------------------------- 
#### **Database Updates:**
Performed CRUD operations using PyMongo.
````
db.establishments.update_many(
 {'BusinessName':'Penang Flavours'},
     {'$set':{'BusinessTypeID': 1}})

establishments.delete_many({'LocalAuthorityName': "Dover"})
````

---------------------------------------------------         
#### **Exploratory Analysis:**
I addressed the following inquiries during the exploratory analysis:

1. Identified establishments with a hygiene score of 20.
2. Identified establishments in London with a RatingValue greater than or equal to 4, utilizing `regex` to search for London.
````
query = {'LocalAuthorityName': {'$regex':'London'}, 'RatingValue': {'$gte':'4'}}
````
3. Determined the top 5 establishments with a RatingValue of 5, sorted by the lowest hygiene score, with priority given to those closest to the "Penang Flavours" restaurant.
````
degree_search = 0.01
latitude = 51.49014200  
longitude = 0.08384000  

query2 = {
    'geocode.latitude': {'$gte': latitude - degree_search, '$lte': latitude + degree_search},
    'geocode.longitude': {'$gte': longitude - degree_search, '$lte': longitude + degree_search},
    'RatingValue': 5
}
    
sort = [('scores.Hygiene', 1)]
limit = 5
results = list(establishments.find(query2).sort(sort).limit(limit))
````
4. Calculated the number of establishments in each Local Authority area that have a hygiene score of 0, and presented the results in descending order, listing the top ten local authority areas. This was achieved using `aggregation` methods.
````
match_query = {'$match': {'scores.Hygiene':0}}
group_query = {'$group': {'_id': {"LocalAuthorityName": "$LocalAuthorityName"},'count': { '$sum': 1 }}}
sort_values = {'$sort': { 'count': -1 }}
pipeline = [match_query, group_query, sort_values]`
results = list(establishments.aggregate(pipeline))
````

