

# Colab Notebook for Data Cleaning and Processing

This notebook demonstrates a series of steps for processing a large CSV dataset within a Google Colab environment. It includes functionalities like splitting large files, cleaning column headers, identifying garbage data (rows with missing or invalid data), and logging the process.

## Steps:

1. **Import Libraries:** 
   - Import necessary libraries like `pandas`, `csv`, `os`, `logging`, and `re`.

2. **Read the CSV:**
   - `df = pd.read_csv("/content/3.6M-Japan-lifebear.com-Largest-Notebook-App-UsersDB-csv-2019.csv", sep=';', low_memory=True)`: Reads a CSV file into a pandas DataFrame.
   - The `sep=';'` argument specifies that the CSV file uses semicolons as delimiters.
   - `low_memory=True` is used to handle large datasets effectively.

3. **Split Large CSV:**
   -  `split_csv(input_file, output_dir, chunk_size)`: defines a function to split a large CSV into smaller chunks.
   - It reads the input file in chunks and creates individual CSV files for each chunk.
   - The `chunk_size` parameter controls how many rows each output file contains.


4. **Read Split File:**
   - `df = pd.read_csv("/content/split_csv_files/chunk_15.csv", sep=';', low_memory=True)` reads a specific chunk file (in this case, chunk_15.csv) into a dataframe.

5. **Rename Columns:**
   - `header_mapping = { ... }`: A dictionary defines a mapping between the desired column names and the existing column names.
   - It then iterates over the mapping and creates a new DataFrame `new_df` with the updated column names.
   - `new_df.to_csv('cleaned_data_15.csv', index=False)` saves the cleaned data with proper header names to a new CSV file.

6. **Garbage Data Identification:**
   - Logs the process of garbage data detection in a file 'garbage_data_log.txt'.
   - Reads the csv file `df = pd.read_csv("/content/split_csv_files/chunk_15.csv", sep=';', low_memory=False)` 
   - Creates an empty DataFrame to store garbage data (rows with missing or invalid data).
   - Performs various checks for invalid data:
     - `invalid_rows = df[df['id'].isnull()]`: Identifies rows where 'id' is missing.
     - Custom functions are created (`is_valid_email`, `is_valid_birthday`, `is_valid_row`) to check for valid email addresses, birthdays, and check the existence of critical columns.
   - Identifies duplicate rows based on a certain column (e.g., `'id'`).
   - Concatenates the rows identified as garbage data into the garbage DataFrame.
   - The `logging` module is used to log the details of each garbage data identification.
   - Finally, it saves the identified garbage data into a separate CSV file `garbage_data.csv`.



## Code Structure

The notebook's structure is well-defined: 

1. Imports.
2. CSV loading and potential splitting.
3. DataFrame manipulation (renaming columns).
4. Garbage data identification and processing.
5. Logging.


## Potential Improvements

- **Error Handling:** Add comprehensive error handling mechanisms to gracefully manage cases like file not found, invalid CSV format, etc.
- **Data Validation:**  Expand the data validation criteria to include checks for inconsistent data formats, out-of-range values, and other potential inconsistencies.
- **Modularization:** Consider breaking down the cleaning process into smaller, reusable functions for enhanced maintainability.
- **Scalability:** Optimization for handling even larger datasets, including utilizing parallel processing or database-based solutions.
- **Customization:** Make the script more configurable (e.g., specifying criteria for identifying garbage data via input arguments).


This README provides a high-level overview of the notebook's functionality. Feel free to modify and extend it as needed for your specific use case.
