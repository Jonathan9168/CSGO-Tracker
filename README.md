# CSGO-Tracker

Provides a Price Tracking Spreadsheet, Inventory Scraper, and Price Updater for CSGO items.

## Spreadsheet

```
Provides price tracking and metrics on the user's CSGO items.
```

### Example

![image](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/397e875d-df81-4e75-9a44-4b64d01e1535)

### Columns and Metrics

Below is an explanation of each column and metric used in the spreadsheet:

- **Purchase Date:** Date the item was bought.
- **Item:** Item name as seen on the Steam market.
- **Condition:** Wear of the item where applicable.
- **Purchase Platform:** Platform from which the item was bought (e.g., Steam or third-party marketplaces).
- **Purchase Price:** Price at which the item was bought.
- **Current Value [Steam]:** Current lowest Steam market listing price for the item.
- **Current Value % Change:** Percentage change from the last value in the corresponding 'Current Value [Steam]' column.
- **Price Difference:** Difference between the current value and the purchase price.
- **Sold Price:** Price for which the item was sold, where applicable.
- **Current Value Updated:** Denotes whether an item's value was updated. 'y' for successful updates and 'n' for unsuccessful ones (e.g., due to incorrect spelling or error 429).
- **Expected Profit (Steam):** The expected profit that can be realized if unsold items are listed at the Steam market value price, accounting for the ~15% Steam fee.
- **Actual Profit:** The actual profit made from confirmed sales.

### Sorting

![image](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/24e16cd7-d89e-4b6a-945b-7c896392f4e0)

To utilize Excel's built-in sorting and analysis features wihtout including summary boxes on the right:

1. **Select Relevant Columns:** Highlight the relevant column letters.
   
3. **Access the Sort Ribbon:** Navigate to the "Home" tab in Excel's ribbon.

4. **Initiate Sorting:** Click the ```'Sort & Filter'``` ribbon and select ```'Custom Sort'```, the user can then select which column to use as the key along with the sort direction.


## Inventory Scraper [```inventory.py```]


Populates the template file with the user's marketable CSGO inventory items.  

![image](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/8704e88b-ad2e-40dc-8b14-17bb066e60d4)

### File Paths

- **base_path:** By default, the script assumes that ```'base_file.xslx'``` (template) is at the same directory level, if not, change accordingly.
- **file_path_local:** The output directory of the newly created spreadsheet after scraping items, change the output name as desired. 
- **file_path_desktop:** Same file as ```'file_path_local'```.  If the file should also be available on your desktop, you can specify your desktop directory here, or you can simply omit this line if it's not needed.
  
```python
170. base_path = 'base_file.xlsx'
171. file_path_local = 'modified_spreadsheet.xlsx'
172. file_path_desktop = r'C:\Users\<your_user_name>\Desktop\modified_spreadsheet.xlsx'
```

```'base_file.xslx'``` is not overwritten, a new spreadsheet containing the user's item is created at the same directory level as the script and a copy is saved to the desktop (where applicable) via the ```save_excel()``` function.

```python
150. def save_excel():
151.     """Saves the updated Excel file with the original formatting to specified directories"""
152.
153.     wb.save(file_path_local)
154.     wb.save(file_path_desktop)
```

### Chromedriver (attempts to fetch automatically)  

If by chance your Chrome version is very new, you can download the win64 driver from :   
https://googlechromelabs.github.io/chrome-for-testing/#stable

View your Chrome version here: chrome://settings/help

## Price Updater [```csgo.py```]


Updates the user's spreadsheet with the current lowest Steam market price listing values (option A) or CSGO Trader daily/weekly averages (options B and C).  

Option A is prone to rate limits so item requests are throttled by default to one every three seconds.


![image](https://github.com/Jonathan9168/CSGO-Tracker/assets/77795437/a139fdec-4be8-4da1-81e4-8c2c6aa551d1)

### File Paths

- **file_path_local:** By default, the script assumes that the user's spreadsheet is at the same directory level, if not, change accordingly.
- **file_path_desktop:** = Same file as ```'file_path_local'```.  If the file should also be available on your desktop, you can specify your desktop directory here, or you can simply omit this line if it's not needed.

```python
209.    file_path_local = '<file_name>.xlsx'
210.    file_path_desktop = r'C:\Users\<your_user_name>\Desktop\<file_name>.xlsx'
```

The user's original spreadsheet is overwritten and a copy is saved to the desktop (where applicable) via the ```save_excel()``` function.

```python
199. def save_excel():
200.     """Saves the updated Excel file with the original formatting to specified directories"""
201.
202.     wb.save(file_path_local)
203.     wb.save(file_path_desktop)
```

## How To Run

1. ```pip install -r requirements.txt```
2. Configure file paths in ```inventory.py``` and ```csgo.py```
3. ```python inventory.py``` Input your Steam inventory URL when prompted (inventory must be public)
4. Fill in item purchase prices in the generated spreasheet
5. ```python csgo.py``` to update item current values

## Additional Requirements 

- Google Chrome (only for ```inventory.py```)
