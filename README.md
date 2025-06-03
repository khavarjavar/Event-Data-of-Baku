[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Ajy8KP4Y)

# Introduction
# Event data of Baku

- **Github Repo URL** https://github.com/ADA-SITE-ENCE-3503/team-project-team-18
Note that as we did have a name issue we did create a new repo and it is the last one we did create and join.

## Project Background
This project aims to scrape, analyze and predict event-related data, focusing on various aspects such as ticket pricing, availability, and audience preferences. The dataset used for this analysis was scraped by Team 18 from iticket.az, and it contains information about events, ticket pricing, and related features. The goal is to clean the data, perform exploratory analysis, and develop a predictive model to forecast event prices based on certain features like ticket availability, minimum price.

## Structure of files
As we had additional text file to store links of events we scraped , we did push the text file to our repo with name "event_links_data_team_18.txt". Although in instructions file it was not mentioned, we needed to keep the file to store our links safe. As it was used for scraping events from their dynamic pages. Additonally we added zip folder of project to BB and repository.


## Objectives
The primary objectives of this project are:
1. **Web Scraping**: Extract event-related data from websites to compile a comprehensive dataset for analysis. This involves using Python libraries like Selenium to scrape event details, ticket prices, availability, and other relevant information.
2. **Data Cleaning**: Handle missing values, convert data types, and standardize column names to ensure data consistency and usability.
3. **Exploratory Data Analysis (EDA)**: Analyze the data through statistical methods and visualizations to identify trends, patterns, and relationships, helping to gain insights into event categories, pricing strategies, and audience preferences.
4. **Predictive Modeling**: Applied a machine learning model (Linear Regression) to predict the maximum event price based on selected features such as ticket availability, minimum price, and tag count.


## Tools and Libraries
The following tools and libraries were used to carry out the analysis and modeling:
- **Python**: The programming language used for data manipulation, analysis, and modeling.
- **Selenium**:To scarpe from JS page
- **Pandas**: For data cleaning, manipulation, and preparation.
- **Matplotlib and Seaborn**: For data visualization.
- **Scikit-learn**: For machine learning, specifically Linear Regression and model evaluation.
- **Datetime**: For time-related data manipulations.

## Dataset Overview
The dataset used in this project includes various columns such as event categories, ticket prices, available tickets, and event duration. Key columns include:
- `Available Tickets`: The number of tickets available for the event.
- `Minimum Price`: The lowest ticket price.
- `Maximum Price`: The highest ticket price (target variable for prediction).
- `Tag Count`: The number of tags associated with each event, representing its category or theme.
- `Event Start` and `Event End`: The start and end dates of the events, used for time-based analysis.
and other columns

# Part 1
# Web Scraping for Event Data from Iticket.az

This project involves web scraping for extracting event data from Iticket.az using Python libraries like Selenium, BeautifulSoup, and requests. The objective is to scrape the details of events listed on the site and store the extracted data in CSV format for further analysis.

## Requirements

Before running the script, ensure that you have the following dependencies installed:

- `selenium`: To automate web browsing and interact with dynamic content.
- `webdriver_manager`: To manage browser drivers.
- `BeautifulSoup4`: For parsing HTML content.
- `pandas`: To store and manipulate scraped data.
- `requests`: To handle HTTP requests for fetching data.


## 1. Getting Nuxt Data (`nuxt_getting` function)
**Purpose**: This function fetches the JavaScript variable `window.__NUXT__`, which is embedded in the page source and contains structured data about events.

### Process:
- Opens the URL with Selenium in headless mode (without displaying a browser).
- Uses `driver.execute_script('return window.__NUXT__;')` to execute JavaScript in the page and fetch the `window.__NUXT__` object, which holds event data.
- Converts the extracted data into a JSON string, ensuring it's properly encoded and then converts it back into a Python dictionary.
- Returns the `nuxt_data` dictionary for further processing.

**Purpose of Code**: Extract structured data from a JavaScript-heavy webpage.

---

## 2. Loading Events (`load_all_events` function)
**Purpose**: Loads the events dynamically by scrolling down and clicking a "Load more" button.

### Process:
- It continuously scrolls to the bottom of the page and clicks the "Load more" button until a specified number of events is loaded.
- It checks whether the "Load more" button is clickable and interacts with it.
- It counts the events loaded on the page using BeautifulSoup by searching for elements with the class `event-list-item`.

**Purpose of Code**: Simulate user interactions to load more events dynamically and retrieve event links.

---

## 3. Getting Event Links (`get_event_links` function)
**Purpose**: Extracts the URLs of individual event pages.

### Process:
- After loading the page with all events, it uses BeautifulSoup to parse the HTML content.
- It finds all links with the class `event-list-item`, which corresponds to individual event pages.
- It appends the full URL for each event link to a list.

**Purpose of Code**: Collects all the event links to later fetch more detailed information.

---

## 4. Saving Event Links (`run_program` function)
**Purpose**: This function integrates the previous steps and saves the event links into a text file.

### Process:
- It opens the Chrome driver, loads events, collects links, and writes them into `event_links_data_team_18.txt`.

**Purpose of Code**: Automates the process of scraping event links and storing them in a text file for later use.

---

## 5. Scraping Detailed Event Data (`scrape_event_data` function)
**Purpose**: Processes the detailed event data from the `nuxt_data` dictionary.

### Process:
- It extracts key event information, such as price, available tickets, artist URL, event start time, description, and cover images.
- The function handles various nested fields in the `nuxt_data` dictionary to collect relevant event details and formats them into a dictionary.

**Purpose of Code**: Extracts specific details from the JSON data of each event and prepares it for storage.

---

## 6. Creating CSV Headers (`create_columns` function)
**Purpose**: Defines the CSV columns for storing event data.

### Process:
- It creates a CSV file with specific headers that match the fields collected from the event data (e.g., event_name, available_tickets, etc.).

**Purpose of Code**: Sets up a CSV file with appropriate column headers for saving the scraped event data.

---

## 7. Processing Event Links and Saving Data (`process_event_links` function)
**Purpose**: Reads event links from the text file, scrapes the corresponding event data, and writes the results into a CSV file.

### Process:
- It reads the list of event links from the `event_links_data_team_18.txt` file.
- For each link, it calls `nuxt_getting` to fetch the structured event data, processes it with `scrape_event_data`, and appends the results to a list.
- After processing a set of events, it writes the collected data to a CSV file in chunks to avoid memory issues.

**Purpose of Code**: Automates the collection and storage of detailed event data into a CSV file.

---

## 8. Main Function (`main` function)
**Purpose**: It orchestrates the overall scraping process by calling the necessary functions.

### Process:
- It initializes the scraping process by calling `process_event_links` with the event link file and output CSV file as parameters.

**Purpose of Code**: Starts the scraping process and handles event data processing.



# Part 2
## Data Cleaning, Processing, and Analysis

### Overview
This project involves processing and analyzing event-related data scraped by Team 18. The dataset is cleaned and enriched to provide meaningful insights into event trends, ticket pricing, revenue generation, and audience preferences. We utilized Python libraries such as `pandas` for data manipulation, `matplotlib` and `seaborn` for visualizations, and explored various statistical relationships within the dataset.

---

### Data Cleaning
#### Identifying and Handling Missing Values
- **Initial Checks**: Missing values were identified for each column using the `isnull()` function, and their counts were analyzed.
- **Textual Columns**:
  - `age_limit`: Missing values were replaced with a default string, "No age limit specified."
  - `description`: Missing values were filled with "No description available."
- **Verification**: A second round of checks ensured that all missing values were appropriately handled.

#### Renaming and Reordering Columns
- **Standardization**: Column names were renamed for clarity and consistency using a predefined mapping (`column_rename_map`).
- **Reordering**: Columns were reordered logically to group related attributes, such as event details, pricing, and URLs.

#### Data Type Conversion
- **Numerical Columns**: 
  - `Available Tickets`, `Minimum Price`, `Maximum Price`, and `Tag Count` were converted to integers.
- **Datetime Columns**: 
  - `Event Start` and `Event End` were converted to `datetime` format for time-based analysis.

---

### Data Analysis and Visualizations
#### Key Steps and Visualizations
1. **Basic Summary**: 
   - Dataset structure, types, and descriptive statistics were examined for an overall understanding.
2. **Event Categories**: 
   - Bar charts highlighted the distribution of events across various categories.
3. **Revenue Insights**: 
   - Total revenue generated by category was analyzed and visualized.
4. **Time-Based Trends**:
   - Events were grouped by month and day of the week to identify patterns, visualized using line and bar charts.
5. **Event Duration**:
   - Histograms showed the distribution of event durations in hours.
6. **Pricing Analysis**:
   - Histograms and bar charts depicted ticket price distributions and category-wise average prices.
7. **Popular Events**:
   - Events with the highest ticket availability were identified and visualized.
8. **Correlation Analysis**:
   - A heatmap displayed correlations among numerical variables like pricing, ticket availability, and duration.
9. **Age Limit and Categories**:
   - A stacked bar chart explored the relationship between age limits and event categories.
10. **Event Duration vs. Pricing**:
    - A scatter plot with regression lines highlighted the relationship between event duration and maximum ticket price.

---

### Libraries and Techniques
- **Data Handling**: Used `pandas` for reading, cleaning, and organizing the dataset.
- **Visualizations**: Employed `matplotlib` and `seaborn` for intuitive and insightful visualizations.
- **Advanced Techniques**: Grouping, aggregation, and datetime manipulation to extract meaningful trends.

### Results
The cleaned dataset (`processed_data_team_18.csv`) serves as the foundation for various insights, which can help event organizers and analysts make informed decisions. The workflow highlights the importance of structured data cleaning and visualization in deriving actionable insights.



# Part 3
## Predictive Modeling and Evaluation

### Overview
In this part of the project, we applied machine learning techniques to predict the `Maximum Price` of events based on selected numerical features. Using a Linear Regression model, we trained and evaluated the model to understand the relationships between ticket availability, minimum price, and tag count on the maximum price of events. The goal was to build a reliable predictive model and assess its performance using appropriate metrics.

---

### Data Preprocessing
Before applying the model, several preprocessing steps were performed:
1. **Data Loading and Inspection**:
   - The cleaned dataset (`processed_data_team_18.csv`) was loaded into a pandas DataFrame.
   - The first few rows of the dataset were displayed, and data types were checked.

2. **Selection of Relevant Features**:
   - The numerical columns `Available Tickets`, `Minimum Price`, and `Tag Count` were chosen as the independent features (X).
   - `Maximum Price` was selected as the dependent variable (y).

3. **Data Cleaning**:
   - The numeric columns were converted to appropriate numeric types, ensuring all values were usable for modeling.
   - Rows with missing values in the relevant columns were dropped.

4. **Correlation Analysis**:
   - A correlation matrix was computed to understand the relationships between the selected features and the target variable.

---

### Model Development
1. **Feature Matrix (X) and Target Variable (y)**:
   - The features (`X`) were selected from the numeric columns, while the target (`y`) was the `Maximum Price` column.

2. **Data Splitting**:
   - The dataset was split into training (80%) and testing (20%) sets using `train_test_split`.

3. **Standardization**:
   - The features were standardized using `StandardScaler` to ensure they had a mean of 0 and a standard deviation of 1, which is crucial for many machine learning algorithms.

4. **Training the Linear Regression Model**:
   - A Linear Regression model was initialized and trained using the training data (`X_train` and `y_train`).

---

### Model Evaluation
1. **Predictions and Performance Metrics**:
   - The trained model was used to predict the `Maximum Price` on the testing data (`X_test`).
   - The model's performance was evaluated using **Mean Squared Error (MSE)** and **R-squared (R²)** metrics.

2. **Model Coefficients**:
   - The coefficients of the model were displayed to understand the influence of each feature on the predicted `Maximum Price`.

3. **Saving Predictions**:
   - The actual vs predicted values were saved to a CSV file for further analysis and reference.

---

### Visualization
A scatter plot was created to visualize the performance of the model:
- **Actual vs Predicted Values**: The scatter plot shows how well the model's predictions align with the actual values, with a red dashed line representing perfect predictions.

---

### Results
The trained model's performance metrics were as follows:
- **Mean Squared Error (MSE)**: A measure of how close the predicted values were to the actual values.
- **R-squared (R²)**: The proportion of variance in the target variable that is explained by the independent features.

The scatter plot further demonstrated the relationship between the predicted and actual values, with points scattered around the red dashed line indicating accurate predictions.

The model's predictions were saved for future reference and analysis. The results provide valuable insights for event pricing and ticket availability trends.



