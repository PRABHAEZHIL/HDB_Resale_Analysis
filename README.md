# HDB Resale Price Analysis (2012-2024 Q3)
![Screenshot 2024-08-01 123651](https://github.com/user-attachments/assets/35a883de-b85a-46b2-ae36-04833e2d9330)

## HDB Resale Analysis in PowerBI  
# [DashBoard](https://app.powerbi.com/groups/me/reports/bd97f543-142a-4314-9cc3-99aa63b8eaf5/d1284b876aaa72599b39?experience=power-bi&pbi_source=storytelling_addin)
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
Total 5 Data Sets:
    1. HDB Resale DataSet 2017 onwards, 
    2. HDB Resale Data 2012-2018,
    3. RegionSG, 
    4. flat amenities, 
    5. HDB Resale Price Index.
The HDB resale price data and HDB Resale Price Index was downloaded from [Data.gov.sg](https://beta.data.gov.sg/datasets?agencies=Housing+and+Development+Board+%28HDB%29&resultId=d_60a6c3d88483cf63d2063c93771a6aeb),<br> 
Python function that uses [Onemap api](https://www.onemap.gov.sg/apidocs/apidocs) to get the latitude and longitude data of the flats based on address.<br> 
The Script is [here](https://github.com/PRABHAEZHIL/HDB_Resale_Analysis/blob/main/GeoCapstone%20(1).ipynb)

### Data Cleaning
HDB Data Set:<br>
	1. Created remaining lease year by Custom Column `([lease_commence_Date]+99)-[Year]`<br>
		    Year Column created by Column by Example of month Column<br>
	2. Created Address Column by Concatenating blk and street_name column 
		     `Address = [block] & “  “& [street_name]`<br>
       
HDB Resale Price Index:<br>
Created Date column from year-quater<br>
  	1. Extracted Year by using Column by Split <br>
  	2. Created Date Column by formula.<br>
           `Date= Date.EndOfQuarter(#date(Number.FromText([Year])),`<br>
           `if Text.End([Quater],1)='1' then 1 else`<br>
           `if Text.End([Quater],1)='2' then 4 else`<br>
           `if Text.End([Quater],1)='3' then 7 else`<br>
           `10,1)`<br>

Flat Amenities:<br>
	To make relationship between Flat_Amenities table and hdb_resale  table created address column in hdb_resale_date, Merged two table using RIGHT_OUTER_JOIN.

### Data Loading
Date Table is created by using DAX `Date = CALENDAR(DATE(2012,1,1),DATE(2024,12,31))`<br>

25 Measures are created. Few Example as follows <br>
  1. Getting TopRegion with the highest  in Transaction<br>
 
  `  VAR TopTown =
      CALCULATETABLE(
        TOPN(1, 
            SUMMARIZE(ResaleFlatPrice_clean, ResaleFlatPrice_clean[town], "TotalTransaction", COUNT(ResaleFlatPrice_clean[resale_price])),
            [TotalTransaction], 
            DESC
        )
    )
RETURN
    MAXX(TopTown,  ResaleFlatPrice_clean[town])`<br>
    
    2. Getting TowTown with the highest Resale Price Index<br>
    
    ` TopTownRPI = 
	VAR TopTown =
 	   CALCULATETABLE(
   	     TOPN(1, 
    	        SUMMARIZE(ResaleFlatPrice_clean, ResaleFlatPrice_clean[town], "TotalTransaction", SUM(HDBResalePriceIndex[index])),
    	        [TotalTransaction], 
     	       DESC
     	   )
   	 )
	RETURN
  	  MAXX(TopTown,  ResaleFlatPrice_clean[town])`<br>

### DashBoard Highlights
#### Interactive Map to get details of Highest Sold Price and nearest Amenities based on Address.
![Screenshot 2024-07-31 110426](https://github.com/user-attachments/assets/fda8d92c-6e8f-4115-a58c-147f5c648fbe)


#### For Buyers/Investors to compare resale prices of two or more addresses over the years, along with amenities details.
![Screenshot 2024-07-31 110744](https://github.com/user-attachments/assets/9dabe4b3-eed8-4c41-994d-c935f8374ebf)


### Conclusion

In this project custom Tooltip in Map shows the latest highest sold price with the remaining lease year, flat type, and flat area. Comparative data in the buyer Dashboard is useful for investors to compare the resale price over the years and also find the nearest amenities. Key influences show insight factors for the resale price increase.
