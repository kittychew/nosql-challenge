# NoSQL Challenge: UK Food Hygiene Data

## Project Overview

In this project, I evaluated food hygiene rating data provided by the UK Food Standards Agency. The goal was to process and analyze the data for the editors of *Eat Safe, Love* magazine, helping them make data-driven decisions about which establishments to focus on for future articles. This challenge involved working with MongoDB, performing database manipulations, and running various queries and analyses using Python.

## Files and Programs Used

- **establishments.json**: Data file provided by the UK Food Standards Agency containing food hygiene ratings for various establishments across the UK.
- **NoSQL_setup_starter.ipynb**: Jupyter notebook used for database setup, data import, and updates.
- **NoSQL_analysis_starter.ipynb**: Jupyter notebook used for exploratory data analysis.
- **Python**: The primary programming language for this project.
- **PyMongo**: Python library used to interact with MongoDB.
- **Pretty Print (pprint)**: Python library used to format and print query results.

## Setup Instructions

1. **Importing Data**: 
   - Used `mongoimport` command to import the data into MongoDB:
   ```bash
   mongoimport --db uk_food --collection establishments --drop --file establishments.json --jsonArray
   ```

2. **Libraries Installed**:
   - `pymongo`
   - `pprint`
   - `pandas`

3. **MongoDB**: The data was stored and manipulated using MongoDB. The database is named `uk_food`, and the collection is `establishments`.

## Project Structure

The project is divided into three main parts:

### 1. **Database and Jupyter Notebook Setup**: 
   - Import data into MongoDB and prepare the database for analysis.
   - Perform initial checks and verify the data was correctly loaded.

   Example code to check the database and collection:
   ```python
   from pymongo import MongoClient
   import pprint

   # Connect to MongoDB and select the database and collection
   client = MongoClient()
   db = client['uk_food']
   collection = db['establishments']

   # Print the number of documents in the collection
   pprint.pprint(collection.count_documents({}))
   ```

### 2. **Database Updates**: 
   - Insert new restaurant data ("Penang Flavours").
   - Modify the database by adding, updating, and removing documents based on specified criteria.

   Code to insert new data:
   ```python
   # Insert a new document (Penang Flavours) into the establishments collection
   collection.insert_one({
       "name": "Penang Flavours",
       "address": "123 Foodie St, London, UK",
       "rating": 5,
       "score": 100
   })
   ```

   Code to update an existing document:
   ```python
   # Update the hygiene score of 'Penang Flavours'
   collection.update_one(
       {"name": "Penang Flavours"},
       {"$set": {"score": 95}}
   )
   ```

   Code to remove a document:
   ```python
   # Remove a restaurant based on name
   collection.delete_one({"name": "Penang Flavours"})
   ```

### 3. **Exploratory Data Analysis**: 
   In this section, I answer key questions using MongoDB queries and Python analysis:

   **a. Establishments with a hygiene score equal to 20:**
   ```python
   # Find establishments with hygiene score of 20
   query = {"score": 20}
   results = collection.find(query)
   pprint.pprint(list(results))
   ```

   This query retrieves all establishments that have a hygiene score of 20. We use the `find()` method and pass the query to MongoDB to match the criteria.

   **b. London establishments with a RatingValue greater than or equal to 4:**
   ```python
   # Find London establishments with a RatingValue >= 4
   query = {"address": {"$regex": "London", "$options": "i"}, "rating": {"$gte": 4}}
   results = collection.find(query)
   pprint.pprint(list(results))
   ```

   Here, we're looking for establishments in London that have a rating greater than or equal to 4. The `$regex` operator is used to find documents where the address field contains the word "London," and `$options: "i"` makes the regex case-insensitive. The `"$gte": 4` checks for ratings greater than or equal to 4.

   **c. Top 5 establishments with a RatingValue of 5, sorted by hygiene score:**
   ```python
   # Find top 5 establishments with RatingValue of 5 and sorted by hygiene score
   query = {"rating": 5}
   results = collection.find(query).sort("score", -1).limit(5)
   pprint.pprint(list(results))
   ```

   This query retrieves establishments with a `rating` of 5 and sorts the results by the `score` field in descending order (`-1` means descending order). The `limit(5)` restricts the results to the top 5 establishments.

   **d. Number of establishments with a hygiene score of 0, sorted by Local Authority:**
   ```python
   # Find establishments with a hygiene score of 0 and count them per local authority
   query = {"score": 0}
   aggregation_pipeline = [
       {"$match": query},  # Filter documents with hygiene score of 0
       {"$group": {"_id": "$local_authority", "count": {"$sum": 1}}},  # Group by local authority and count occurrences
       {"$sort": {"count": -1}}  # Sort by the count in descending order
   ]
   results = collection.aggregate(aggregation_pipeline)
   pprint.pprint(list(results))
   ```

   In this more complex aggregation query, we're first filtering establishments with a hygiene score of 0 using `$match`. Then, we group the results by `local_authority` and use `$sum` to count the number of establishments in each local authority. Finally, we sort the results by the count in descending order using `$sort`.

   **e. Establishments that are missing the `rating` field:**
   ```python
   # Find establishments with missing 'rating' field
   query = {"rating": {"$exists": False}}
   results = collection.find(query)
   pprint.pprint(list(results))
   ```

   This query searches for establishments where the `rating` field does not exist (`$exists: False`). It helps identify any missing ratings.

   **f. Establishments with a score between 70 and 90, ordered by rating:**
   ```python
   # Find establishments with a score between 70 and 90, sorted by rating
   query = {"score": {"$gte": 70, "$lte": 90}}
   results = collection.find(query).sort("rating", 1)  # Sorting by rating in ascending order
   pprint.pprint(list(results))
   ```

   This query finds establishments with a score between 70 and 90, inclusive. We use `$gte` (greater than or equal to) and `$lte` (less than or equal to) to define the range. The results are then sorted by `rating` in ascending order (`1` means ascending).


## Acknowledgements

Thanks to ChatGPT for assistance with coding and troubleshooting.
