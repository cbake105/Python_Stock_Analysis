# Boeing Stock Analysis

![boeing](https://github.com/cbake105/Python_Stock_Analysis/assets/133677209/eb22c068-b320-41dd-8a67-57b4f90591f0)

## Instructions 

Exercise 1
In this exercise, you will practice importing data stored in a CSV file, viewing records, and setting the index. Note: df is a common reference to a generic DataFrame.
1. Use pd.read_csv() to import the Boeing stock data stored in BA.csv and store the DataFrame in a variable named ‘ba’.
2. Print the DataFrame info.
3. Convert the ‘Date’ column to a DateTime type using pd.to_datetime.
Specify the format using: format=r‘%Y-%m-%d’.
4. Set the index of the DataFrame to be the date column using df.set_index().
- Make sure to pass ‘Date’ instead of ba['Date'] when setting the index; the latter will create a copy of the column.
- Print the info and head to verify the index was set correctly and the column was dropped.

Exercise 2
In this exercise, you will practice extracting data from DataFrames, creating new variables, and merging DataFrames.
1. Import the S&P500 (sp500.csv) and Boeing (ba.csv) data and store as DataFrames named sp500 and ba, respectively.
2. Extract the Open and Close data from both DataFrames and store as separate DataFrames named sp500oc and ba_oc.
3. Calculate the simple and log returns for S&P500 and Boeing using the closing price.
- Use .shift() to create a column (variable) of the previous day’s closing price.
4. Merge the two DataFrames into a new DataFrame.
5. Print the mean and standard deviation of the log and simple returns; format the output professionally.

Exercise 3
In this exercise, you will practice extracting data from DataFrames, creating new variables based on conditions, and merging DataFrames.
1. Extract the Open and Close data from both DataFrames and store as separate DataFrames named sp500oc and ba_oc.
2. Create a variable named ‘Pos_Day’ where the value is true if the stock/index had a positive day.
3. Merge the two DataFrames into a new variable.
4. Create a new variable that is equal to 1 if Boeing had a positive day and S&P500 had a negative day.
5. Print the number of times Boeing closed positive and the S&P closed negative using .value_counts().
- Create a new column that keeps track of the days; use 1 or True, and 0 or False.
- Apply the .value_counts() method to this column inside a print function.


Exercise 4
In this exercise, you will practice joining data that has gaps.
1. Import the Blackberry stock data from NYSE and TSE into separate DataFrames.
2. Extract only the data for January 2018; you can reassign the extracted data to the same variables.
3. Create a new DataFrame that is the TSE data joined with the NYSE data.
- Use .join() and don’t forget to specify suffixes ‘_tse’ and ‘_nyse’.
4. Print the slice that is between January 12th and January 17th. How was the gap handled?

Exercise 5
In this exercise, you will practice renaming columns and creating lagged and moving average variables.
1. Import the S&P500 data into a DataFrame.
2. Rename the columns so that they are all lowercase and spaces are replaced with ‘_’.
- This can be done using a loop and the .lower() and .replace() methods.
3. One measure of volatility is the weighted average of the squared return of the previous day close to current day open and the squared return of the current day open to current day close.
- Create a variable that is the previous day close using the shift function.
- Calculate the log return of the previous day close to current day open; store this value in a variable named ‘log_rtn_c_to_o’.
- Calculate the log return of the current day open to the current day close; store this value in a variable named ‘log_rtn_o_to_c’.
- Create variables named ‘vol_c_to_o’ and ‘vol_o_to_c’ which are the squares of ‘log_rtn_c_to_o’ and ‘log_rtn_o_to_c’ respectively.
- Create a variable that represents the weight applied to the close to open volatility; set the variable to 0.5.
- Calculate the weighted average of ‘vol_c_to_o’ and ‘vol_o_to_c’ and store the value in a variable named ‘vol’.
4. Create a lagged variable of ‘vol’ named ‘vol_1’.
5. Create variables that are the 5-day and 22-day moving average of ‘vol’ named ‘vol_ma_5’ and ‘vol_ma_22’ respectively.
- Use .rolling() and the .mean() methods on ‘vol_1’.
6. Print the first 30 records using .head() and save the DataFrame to a file.

Exercise 6
In this exercise, you will practice merging data of different frequencies and creating variables using financial report data.
1. Import the Boeing stock data into a DataFrame.
- Convert the header to lowercase and replace the spaces with ‘_’.
- Convert the ‘date’ column to DateTime.
2. Import the financials data that is stored in ‘fundamentals.csv’ into a DataFrame named ‘financials’.
- Convert the header to lowercase and replace the spaces with ‘_’.
- Convert the ‘period_ending’ column to DateTime.
3. To avoid matching data that technically would not have been available, create another date variable to match along by offsetting it by three months.
- Use either pd.offsets.MonthEnd(-3) for the stock data or pd.offsets.MonthEnd(3) for the financial data to create a ‘match_date’ variable.
4. Create a variable in the ‘financials’ DataFrame named ‘roa’ which is calculated by dividing Net Income by Assets.
5. Perform a left merge on the DataFrame containing the Boeing data with the financial data, selecting only data where ‘ticker_symbol’ equals ‘BA’ and selecting only the ‘match_date’ and ‘roa’ columns. Store this in a new DataFrame variable called ‘ba_fin’.
6. Fill in the NAs using the .fillna(method='ffill') method.
- Filter the ‘ba_fin’ DataFrame to only include dates less than or equal to the ‘max_date’ and greater than or equal to the ‘min_date’.
7. Print .info() to see if there are any NAs in the ‘roa’ column. Challenge: Repeat the steps above but use the .drop_na() method instead of filtering using the ‘min_date’ variable.

Exercise 7
In this exercise, you will practice resampling data frequency and merging factor data.
1. Load the Boeing stock data into a DataFrame.
- Convert the header to lowercase and replace the spaces with ‘_’.
- Convert the ‘date’ column to DateTime.
2. Load the Fama-French 3-Factor data stored in FF3.csv in a DataFrame called ‘ff3’.
- Convert the ‘date’ column to DateTime and offset to the current month end.
3. Create a dictionary that contains the rules for resampling: ohlc_rule = {'open':'first', 'high':'max', 'low':'min', 'close':'last', 'volume':'sum', 'adj_close':'last'}
4. Resample the daily Boeing data to monthly using the ‘ohlc_rule’. Assign the resampled data to ‘ba_mon’.
5. Calculate log or simple returns for ‘ba_mon’ using the ‘adj_close’ variable.
6. Perform a merge on the ‘ba_mon’ DataFrame with the ‘ff3’ DataFrame.
7. Print the first five records using .head().
- Correct the scale problem by multiplying the returns by 100.
