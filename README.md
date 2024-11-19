# NoSQL Challenge: UK Food Hygiene Data

# Eat Safe, Love

A MongoDB-based project for analyzing and maintaining the UK Food Establishments database. This project demonstrates database setup, CRUD operations, and data cleaning using Python and PyMongo.

## Table of Contents
1. [Project Overview](#project-overview)
2. [Technologies Used](#technologies-used)
3. [Setup Instructions](#setup-instructions)
4. [Key Features](#key-features)
5. [Code Overview](#code-overview)
6. [Project Highlights](#project-highlights)
7. [Future Improvements](#future-improvements)
8. [License](#license)

---

## Project Overview

The purpose of this project is to showcase the ability to work with large datasets in a MongoDB database. Specifically, the project involves:
- Setting up a MongoDB database for food establishments in the UK.
- Performing CRUD (Create, Read, Update, Delete) operations on the data.
- Cleaning and transforming data for analysis.
- Writing Python scripts for database interactions.
- Preparing the database for further analysis in future applications.

---

## Technologies Used

- **Python**: For scripting and interacting with MongoDB.
- **PyMongo**: MongoDB driver for Python.
- **MongoDB**: NoSQL database for handling unstructured data.
- **Jupyter Notebook**: Interactive development environment.
- **Git**: Version control for code management.
- **Terminal/Command Line**: For database imports and interaction.

---

## Setup Instructions

### Prerequisites
1. Install Python 3.8 or higher.
2. Install MongoDB (ensure the server is running on `localhost:27017`).
3. Install the required Python libraries:
    ```bash
    pip install pymongo jupyterlab
    ```

4. Download the `establishments.json` dataset from the `Resources/` folder.

### Steps
1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/eat-safe-love.git
    cd eat-safe-love
    ```

2. Import the dataset into MongoDB:
    ```bash
    mongoimport --db uk_food --collection establishments --drop --file Resources/establishments.json
    ```

3. Launch the Jupyter Notebook to run the analysis:
    ```bash
    jupyter notebook
    ```

4. Open the `Eat_Safe_Love.ipynb` notebook and follow the steps to interact with the database.

---

## Key Features

### Database Setup
- Import data into MongoDB.
- Verify database creation and data structure.

### CRUD Operations
- **Create**: Insert new restaurant data into the database.
- **Read**: Query data using specific fields and conditions.
- **Update**: Modify existing records, including geolocation updates.
- **Delete**: Remove data based on specific criteria.

### Data Cleaning
- Standardize data types for latitude, longitude, and rating values.
- Handle non-numeric entries in the `RatingValue` field.

### Analysis-Ready Data
- Prepare the database for future analysis by ensuring the data is clean, structured, and accessible.

---

## Code Overview

The project is organized into several steps for clarity:

1. **Part 1: Database Setup**
   - Import the dataset.
   - Verify database and collection structure.
   - Connect to MongoDB using PyMongo.

2. **Part 2: Update the Database**
   - Insert new data for a restaurant.
   - Query for specific fields (e.g., `BusinessTypeID`).
   - Perform updates for geolocation and data type transformations.
   - Delete specific entries based on criteria (e.g., establishments in Dover).

3. **Part 3: Data Cleaning**
   - Convert string fields (`latitude`, `longitude`, `RatingValue`) to appropriate numeric types.
   - Handle non-numeric entries gracefully.

Each operation is performed programmatically using PyMongo, with results verified after each step.

---

## Project Highlights

- **Data Cleaning**: Demonstrated ability to handle real-world data challenges, such as inconsistent data types and missing values.
- **CRUD Mastery**: Performed all key database operations (Create, Read, Update, Delete) with real-world use cases.
- **Documentation**: Comprehensive documentation ensures reproducibility and clarity for future users and collaborators.
- **MongoDB Skills**: Showcased proficiency with NoSQL databases and Python integration.

---

## Future Improvements

- **Data Visualization**: Integrate Matplotlib or Seaborn to visualize trends in the data.
- **Web Interface**: Create a frontend using Flask or Django for easier interaction with the database.
- **Automated Testing**: Add unit tests to ensure database operations are error-free.
- **Scalability**: Optimize queries for performance with indexing and aggregation pipelines.

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---

## Acknowledgements

Thanks to ChatGPT for assistance with coding and troubleshooting.
