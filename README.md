
# Stock Screener Dashboard

## Objective
The goal of this project is to develop a dashboard that allows users to evaluate stocks based on their fundamental data and historical performance. Users can select a stock and view relevant data and performance through pre-compiled reports.

## Data Definitions

### Universe Data
- **symbol**: Unique identifier for a company or financial instrument.
- **name**: Name of the company or financial instrument.
- **price**: Current price of the company's stock or financial instrument.
- **exchange**: Name of the exchange where the stock is traded.
- **exchangeShortName**: Abbreviated name of the exchange.
- **type**: Category or type of the company.

### Company Fundamental Data
- **symbol**: Unique identifier for a company or financial instrument.
- **price**: Current price of the company's stock or financial instrument.
- **beta**: Measure of the stock's volatility relative to the market.
- **volAvg**: Average trading volume over a specified period.
- **mktCap**: Market capitalization of the company.
- **lastDiv**: Last dividend paid by the company.
- **range**: Price range over a specified period.
- **changes**: Change in price over a specified period.
- **companyName**: Name of the company.
- **currency**: Currency in which the stock is traded.
- **cik**: Central Index Key used to identify securities.
- **isin**: International Securities Identification Number.
- **cusip**: Committee on Uniform Securities Identification Procedures number.
- **exchange**: Name of the exchange where the stock is traded.
- **exchangeShortName**: Abbreviated name of the exchange.
- **industry**: Industry in which the company operates.
- **website**: Company's website URL.
- **description**: Description of the company or financial instrument.
- **ceo**: Name of the company's Chief Executive Officer.
- **sector**: Sector in which the company operates.
- **country**: Country in which the company is headquartered.
- **fullTimeEmployees**: Number of full-time employees.
- **phone**: Contact phone number of the company.
- **address**: Address of the company.
- **city**: City where the company is located.
- **state**: State where the company is located.
- **zip**: Postal code of the company's location.
- **dcfDiff**: Difference between Discounted Cash Flow (DCF) valuation and price.
- **dcf**: Discounted Cash Flow (DCF) valuation.
- **image**: URL of the company's logo or image.
- **ipoDate**: Date of the company's Initial Public Offering (IPO).
- **defaultImage**: URL of a default image for the company.
- **isEtf**: Boolean indicating if the company is an Exchange-Traded Fund.
- **isActivelyTrading**: Boolean indicating if the company's stock is actively traded.
- **isAdr**: Boolean indicating if the company is an American Depositary Receipt (ADR).
- **isFund**: Boolean indicating if the company is a fund.

### Stock Price Data
- **Date**: Date of the trading day.
- **Open**: Opening price of the stock during the trading day.
- **High**: Highest price of the stock during the trading day.
- **Low**: Lowest price of the stock on the trading day.
- **Close**: Closing price of the stock on the trading day.
- **Volume**: Number of shares traded on the trading day.
- **Dividends**: Dividends paid on the trading day.
- **StockSplits**: Stock splits that occurred on the trading day.
- **symbol**: Symbol of the company (ticker).

## Technical Stack
- **AWS Cloud Services**
  - **EC2**: Elastic Compute Cloud
  - **Redshift**: Cloud-based data warehousing service
  - **S3**: Object storage service
- **Python**: Programming language used for data processing
- **Tableau**: Data visualization software used for dashboarding

## Architecture

### Daily Process
1. **Data Ingestion**: A Python script runs daily at 5:45 PM CST, fetching data from Financial Modeling Prep and Yahoo Finance APIs, then uploads it to an S3 bucket.
2. **Data Insertion**: At 6:00 PM CST, a script inserts the data from the S3 bucket into a Redshift table.
3. **Dashboard Refresh**: Tableau dashboard refreshes daily at 7:00 PM CST using the updated data.

### Data Ingestion Script
- Fetches company profile and price history data.
- Saves data into CSV files, organizes them into directories by date, and uploads to S3.

### Data Insertion Script
- Runs after the ingestion script.
- Loads CSV data from S3 into Redshift.

## AWS Services Configuration

### EC2 Instance
1. **Launch Instance**: Choose a Linux AMI.
2. **Configure Instance**: Select t2.micro, configure network, and security settings.
3. **Add Storage**: Attach an EBS volume.
4. **Configure Security Group**: Set inbound/outbound rules.
5. **Create Key Pair**: Generate a key pair for SSH access.

### S3 Bucket
1. **Create Bucket**: Provide a unique name and configure permissions.

### Redshift Cluster
1. **Create Cluster**: Choose a single node of dc2.large.
2. **Configure Security**: Ensure the cluster is publicly accessible and configure security groups.
3. **Create Tables**: Use SQL commands to create required tables.

## Initial and Daily Loads

### Initial Load
- Uses CSV files from the "full_load" folder to load data into Redshift.

### Daily Load
- Creates directories for the date and downloads data into them.

## Visualizations

### Overview Tab
Displays a table of stock tickers, including open/close price, volume, and percentage change.

### Stock Screener Tab
Provides a candlestick chart for analyzing stock trends.

### Market Capitalization by State
Visualizes market cap distribution across different states.

### Volume Comparison of Different Stocks
Compares trading volume of different stocks over time.

### Market Capitalization by Sector
Visualizes market capitalization by sector with a color gradient.

## Automated Data Refresh
1. **Redshift Cluster Refresh**: Daily at 6:00 PM.
2. **Tableau Dashboard Refresh**: Automatically updates after Redshift refresh.

## Contact
For more information, contact [Your Name] at [Your Email Address].
