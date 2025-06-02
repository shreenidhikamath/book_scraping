#  Book Data Scraping Report

##  Introduction
This project focuses on scraping book details from [Books to Scrape](http://books.toscrape.com/) using Python. The goal is to analyze trends in **pricing**, **ratings**, and **stock availability** by collecting data programmatically and storing it in a structured format.



##  Objectives
- Extract **Title**, **Price**, **Availability**, **Rating**, and **Product URL** for ~1000 books.
- Save data to a structured CSV file (`books_data.csv`).
- Handle missing or malformed data with robust error handling.
- Validate extracted data using basic test cases.


##  Technologies Used
- **Programming Language**: Python  
- **Web Scraping**: `requests`, `BeautifulSoup`  
- **Data Handling**: `pandas`  
- **Logging**: Python’s built-in `logging` module  
- **Storage Format**: CSV



##  Business Flow
1. **Initiate Scraping** – Start from the homepage.
2. **Send HTTP Request** – Validate response code (200 OK).
3. **Extract Data** – Scrape book attributes (Title, Price, Rating, Availability, URL).
4. **Handle Pagination** – Navigate through all pages.
5. **Log Errors** – Capture and record issues like missing fields or HTTP failures.
6. **Store Data** – Save cleaned and structured data in `books_data.csv`.
7. **Validate Data** – Run tests for structure and integrity.



##  Web Scraping Process
- The scraper fetches page content and parses book details from well-defined HTML elements.
- Text-based ratings (e.g., “One”, “Two”) are mapped to numeric values for consistency.
- The scraper loops through all pages dynamically to ensure comprehensive coverage.
- Final data is cleaned and stored as a CSV file for analysis.



##  Code Structure & Key Functions

### 1. `fetch_page(url)`
- Sends HTTP GET request.
- Validates the status code.
- Implements timeout and error handling.

### 2. `process_books(book_list, books)`
- Parses book attributes and formats them into dictionaries.
- Handles missing fields and converts rating strings to integers.
- Appends valid entries to the main data list.

### 3. `scrape()`
- Coordinates pagination and book extraction.
- Calls helper functions like `fetch_page()` and `process_books()`.
- Stops gracefully if an error or end-of-data condition occurs.

### 4. `save_to_csv(books)`
- Uses `pandas` to convert book data into a DataFrame.
- Saves the final dataset to `books_data.csv`.



## ⚠ Error Handling

| Type                     | Handling Strategy                                                              |
|--------------------------|---------------------------------------------------------------------------------|
| Missing Data             | Skips invalid books and logs an error.                                         |
| HTTP Errors              | Retries request; logs persistent failures to `scraping_errors.log`.            |
| Invalid Rating Format    | Sets rating to `None` and logs the issue.                                      |
| Empty Page Response      | Terminates the pagination process gracefully.                                  |

**Logging Example:**
```python
logging.error(f"Skipping book due to missing data: {e}")
