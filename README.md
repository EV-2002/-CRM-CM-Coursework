# -CRM-CM-Coursework


What this is
------------
This folder has my CRM coursework. I grouped S&P 500 shares in two ways:
 
  1. Risk-return: average weekly return and beta (2021 to 2024)
  2. Trading activity: Recency, Frequency and Monetary (RFM) over the
     last 60 trading days of 2024
 
The notebook does all the data work. The report explains the results.
 
 
What's in the folder
--------------------
  CRM_Coursework.ipynb         the notebook (all the code)
  CRM_Coursework_Report.docx   the written report
  README.txt                   this file
  requirements.txt
When you run the notebook it also creates two folders:
 
  data/      the ticker list, the downloaded prices and a metadata file
  outputs/   result tables (CSV/Excel), the run manifest and all charts
 
 
How to run it
-------------
I built and ran the notebook in Google Colab.
 
  1. Open the notebook in Colab (or Jupyter).
  2. Click Runtime > Run all.
  3. Wait a few minutes. Most of the time goes on downloading prices.
 
Please run the cells in order from the top. Later cells use results
from earlier ones, so a single cell on its own will not work.
 
You need an internet connection, because the ticker list comes from
Wikipedia and the prices come from Yahoo Finance (through yfinance).
 
If you run it outside Colab, install these first:
 
  pip install pandas numpy yfinance scikit-learn scipy matplotlib seaborn lxml openpyxl
 
 
Getting the same numbers as the report
---------------------------------------
The numbers in the report come from a run on 20 November 2026.
A new run downloads fresh data, so some figures may change slightly
(Yahoo updates adjusted prices and the S&P 500 list changes over time).
 
To get exactly the same results, use the saved data instead of a new
download. In cell 2, replace the download line with:
 
  raw_data = pd.read_csv('data/raw_data.csv.gz', header=[0, 1], index_col=0, parse_dates=True)
 
The clustering uses a fixed seed (42), so it gives the same groups
on the same data every time.
 
 
Main settings
-------------
  Price period      1 Jan 2021 to 31 Dec 2024
  Shares used       486 (17 removed for missing or bad data)
  RFM window        7 Oct to 31 Dec 2024 (60 trading days)
  High-volume day   volume more than 2x the average of the previous 20 days
  Clustering        Ward and K-means, 4 clusters each
 
 
Things to know
--------------
- yfinance is not an official Yahoo tool. A few tickers return no data
  and are listed in outputs/inclusion_exclusion_log.csv.
- I used today's S&P 500 list for past years, so companies that left
  the index are missing (survivorship bias).
- You may see a Matplotlib warning about boxplot labels. It doesn't
  affect the results.
- The clusters describe past behaviour. They are not investment advice.
 
