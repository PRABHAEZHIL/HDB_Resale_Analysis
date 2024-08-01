# HDB Resale Price Analysis (2012-2024 Q3)
![Screenshot 2024-08-01 123651](https://github.com/user-attachments/assets/35a883de-b85a-46b2-ae36-04833e2d9330)

## HDB Resale Analysis in PowerBI  [DashBoard](https://app.powerbi.com/groups/me/reports/bd97f543-142a-4314-9cc3-99aa63b8eaf5/d1284b876aaa72599b39?experience=power-bi&pbi_source=storytelling_addin)
### The Project Goal
____
This project explores the trends and factors influencing HDB (Housing Development Board) resale prices in Singapore. By analyzing historical data, we'll uncover insights to help homebuyers and investors make informed decisions in the HDB resale market.

#### Research Objective Takeaway 
The 8 pages of Power BI project and their functionality are as follows:

  1. Resale trends over years and uncover   more about the future Using Forecast AI
  2. Hierarchical distribution of Resale Prices across Regions, Towns, Blocks and so on.
  3. HDB resale prices and sales volumes from 2012 to 2024, highlighting key factors influencing these metrics.
  4. Overview of HDB resale transactions, showcasing the total transaction value and key statistics and  transaction volumes across different towns.
  5. Offers Valuable insights for Property market stakeholders by the resale price index values over the years
  6. Interactive Map to help to find out the nearest MRT, school, mall, and latest Highest Resale Price of the Blk.
  7. For Investors to get the Latest resale prices over the years with the Nearest Amenities values.
  8. Multivariate clustering analysis performed using machine learning techniques in Power BI.

### Data Extraction
5 Data Sets Used HDB Resale DataSet 2017 onwards, HDB Resale Data 2012-2018, RegionSG, flat amenities, HDB Resale Price Index.
The HDB resale price data and HDB Resale Price Index was downloaded from [Data.gov.sg](https://beta.data.gov.sg/datasets?agencies=Housing+and+Development+Board+%28HDB%29&resultId=d_60a6c3d88483cf63d2063c93771a6aeb), 
To retrieve the latitude and longitude data of the flats based on address the [Onemap api](https://www.onemap.gov.sg/apidocs/apidocs).\ 
The Script is [here](GeoCapstone (1).ipynb)

