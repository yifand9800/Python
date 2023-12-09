
# CarBoost

CarBoost is a platform aimed at optimizing user experience in searching for information of used car. CarBoost integrates data from CarMax, Reddit and Youtube.

## Team Information

Wenqi Shen | ID: wenqishe

Yifan (Iris) Dai | ID: yifandai

Haodong Zhang | ID: haodong3

David (Zexin) Zou | ID: zexinz

Mikee (Mingqi) Zeng	| ID: mingqiz

## Data Source and Data Cleaning

This process involves extracting stock information from CarMax Website to generate car's information table. Considering for the complexity of the scraping problem, we are inspired by the original code from one [project](https://github.com/purvasingh96/Data-Collection-for-CarZam/tree/main). The original code from this repository has been modified for our specific data collection and cleaning process.

Since the web data is real-time changing, please do not try to run it one more time as it could generate different results and datasets from our project. Also, the web scraping process may take 10-15 minutes. To save time, please refer to our generated data table [stock_info.csv](./CarMax_Data_Collection/utils/stock_info.csv).

### Pre-requisites
* Make sure you have ***Python 3.11*** running on your machine.
* Other third party libraries that are required to be downloaded for the project: pandas, selenium, furl, logging, math, json, time.

### Extracting and Cleaning Vehicle Stock Information
Python script, [car_schema_scrapper_util.py](./CarMax_Data_Collection/utils/car_schema_scrapper_util.py) extract relevant data from the CarMax. To run the same, simply run the main function of the class:<br>

#### Usage
```python
if __name__ == '__main__':

        original_skip_value = params["skip"]

        driver = webdriver.Chrome()

        driver.get(buildCompleteUrl())

        # region Display total CarMax listings
        totalListingsToGet = retrieveJsonDataFromWebdriver()["totalCount"]
        print("Listings to scrape: " + str(totalListingsToGet))

        logging.info("STARTED Scraping " + str(totalListingsToGet) + " listings")

        for i in range(math.floor(totalListingsToGet / 1000)):
            driver.get(buildCompleteUrl())

            appendItemsToSaleList(retrieveJsonDataFromWebdriver())

            time.sleep(0.4)

            params["skip"] += 1000

        params["take"] = (totalListingsToGet % 1000)

        driver.get(buildCompleteUrl())
        appendItemsToSaleList(retrieveJsonDataFromWebdriver())

        final_file_name= 'vehicle_features.csv'
        csv.exportCSV(final_file_name, allItemsForSale)

        print("Exported all listings to " + exportCSVFilename)
        params["skip"] = original_skip_value
```
<br>

There will be one CSV file generated after the data web scraper completes its crawling successfully, [stock_info.csv](./CarMax_Data_Collection/utils/stock_info.csv). 

To get a filtered data, Python script, [data_cleaning.py](./CarMax_Data_Collection/utils/data_cleaning.py) extract useful columns from the scraped data in [stock_info.csv](./CarMax_Data_Collection/utils/stock_info.csv). To run the same, simply run the main function of the class:<br>

#### Usage
```python
if __name__ == '__main__':
    #print(selected_df)

    output_file = 'stock_info_cleaned.csv'  # You can change the file name and path as needed
    selected_df.to_csv(output_file, index=False)  # Set index=False if you don't want to include row indices

    print(f"Data saved to {output_file}")
```
<br>

There will be one CSV file generated after the data cleaning completes its crawling successfully, [stock_info_cleaned.csv](./CarMax_Data_Collection/utils/stock_info_cleaned.csv). 


## Installation

### 1. Install the required python modules
To install the python modules needed in the project, run the following command in terminal/console
```bash
pip install -r requirements.txt
```

### 2. Run the main program
The entry of the project is `user_interface.py` . Run it directly in an IDE or run the following command:
```bash
python3 user_interface.py
```

You should see the GUI after running the main program.

## Usage

See the following video for how to use the program:
https://www.youtube.com/watch?v=XUw_Gyhlw9A
