import pandas as pd
import os


# Define the folder where your CSV files are
csv_folder = "C:\Users\8787\Documents\P\nova ext\ResumoBalanco\csvv"  # Replace with your folder path, e.g., "C:\\Users\\YourName\\Documents\\CSVFiles"


# Step 1: Load the expected column names from a reference file
with open('layout_Balanco.txt', 'r', encoding='utf-8') as f:
    expected_columns = [line.strip() for line in f if line.strip()]



# Step 2: Function to find which row has the headers
def find_header_row(file_path, expected_columns, max_rows=5):
    for i in range(max_rows):
        # Read just one row at a time, starting from row i, without assuming a header
        df_temp = pd.read_csv(file_path, header=None, nrows=1, skiprows=i)
        # Check if this row matches the expected column names
        if list(df_temp.iloc[0]) == expected_columns:
            return i  # Return the row number where the header was found
    return None  # If no match is found in the first few rows

# Step 3: Process each CSV file
file_names = ['file1.csv', 'file2.csv', 'file3.csv']  # Replace with your list of files
dfs = []  # List to store the dataframes

# Step 2: Generate list of 40 CSV file names
file_names = ['data.csv'] + [f'data ({i}).csv' for i in range(1, 49)]
print(f"Reading {len(file_names)} files: {file_names[:5]}...")  # Show first 5 for confirmation


for file in file_names:
    try:
        # Find the header row for this file
        header_row = find_header_row(file, expected_columns)
        if header_row is not None:
            # Read the CSV, using the detected header row as column names
            df_temp = pd.read_csv(file, header=header_row)
            dfs.append(df_temp)
            print(f"Processed {file} with header on row {header_row + 1}")
        else:
            print(f"Warning: Could not find header in {file} within the first 5 rows. Skipping.")
    except Exception as e:
        print(f"Error reading {file}: {e}")

# Step 4: Combine all dataframes (if needed)
if dfs:
    combined_df = pd.concat(dfs, ignore_index=True)
    # Add any further cleaning or sorting here
    print("All files combined successfully!")
else:
    print("No valid files were processed.")
