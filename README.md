## Introduction
This is for Guzman Energy 2020-21 Winter Full-Time/Part-Time Quant Internship recuriting. 
- **Assignment 1-3 are required**. Assignment 4 is optional.
- You can use either R or Python **(Recommended)** for coding.
- Requirements:
  - create your own github repository for result delivery
  - PDF summary report for each assignment is required.
  - for python, create jupyter notebook file
- **Due: before November 17th, 2020 5pm ET.** early delivey is welcomed.
- Hints:
  - make your code neat and self explanatory
  - in summary report, provide your insights and conclusions

## Assignment 1: Power Calendar function
#### Objective: write R/Python function which returns number of hours by iso/peak.type/period
In power market, the industry defines certain hour of each day to peak type for block trading, so we need to calculate correctly how many hours belongs to certain block. Each ISO has a little different definition of it. 
- See reference: https://www.energygps.com/HomeTools/PowerCalendar

#### Required Function: get.hours(iso, peak.type, period)
###### Params: (all params are required in the function)
-	iso (character): one of PJM/MISO/ERCOT/SPP/NYISO/WECC/CAISO (see item 1 below)
-	peak.type (character): one of onpeak/offpeak/flat/2x16H/7x8
-	period (character): has 4 types: “2018-2-3” as a daily, “2018Mar” as a monthly, “2018Q2” as a quarterly, “2018A” as an annually.
###### Return:  a list variable giving iso/peak.type/start.date/end.date/num.hour where num.hour is the total number of hours of that peak type in that period.
```R
##### Sample Run #####
> num.hours.ercot.onpeak.may19 <- get.hours("ERCOT", "onpeak", "2019May")
> num.hours.ercot.onpeak.may19
$`iso`
[1] "ERCOT"
$peak.type
[1] "onpeak"
$start.date
[1] "2019-05-01"
$end.date
[1] "2019-05-31"
$num.hour
[1] 352
```
#### Hint:
1.	In US, there are 7 major ISOs (PJMISO, MISO, ERCOT, SPPISO, NYISO are eastern, WECC and CAISO is western.) see https://www.ferc.gov/industries/electric/indus-act/rto.asp
2.	HE, short for Hour Ending. HE2 means 01:00 - 02:00, HE14 means 13:00 - 14:00. For each single day, we have HE1 to HE24.
3.	peak.type, eastern power market considers a HE to be onpeak, if it's a non-NERC holiday weekday from HE7 to HE22, the rest are offpeak HEs. If the peak.type is flat, that means every hour. (Hint, R package “timeDate” gives NERC holidays). 2x16H is HE7 to HE22 for the weekend and the NERC holiday. 7x8 is non HE7 to HE22 through the week. 
4.	Western market accepts all the assumptions from Eastern, moreover, it takes Saturday as a weekday.
5.	MISO does not have the daylight-saving setting, the rest have. (Hint: daylight-savings will impact the function for certain month/peak.type.)

## Assignment 2: Meter Data formatting
#### Objective: merge different data sources into single dataset and evaluate the dataset for anormaly (if any)
For analysis purpose, we always have different data sources to merge and format. It’s important to understand the data and format it correctly. 
#### Data Files:
-	**USA_AL_Auburn-Opelika.AP.722284_TMY3_BASE.csv**
  This file gives hourly electricity consumptions for a resident with unit in kw (kilowatt). 
-	**new.app4.csv**
  Assuming this is one appliance’s electricity consumption minute by minute which is not captured in the previous file. 
  The unit in the file is in watt.
#### Requirements:
-	**for R, use R dplyr package; for Python, use dfply package**
- Create script to load both files and merge.
-	Given the limitation of data period, try to find the overlap period and merge the data into hourly. (ignore the year but making sure the date/hour matched)
-	After merging the source files correctly, please create one more column in the output file to give total hourly consumption of electricity. (sum all columns)
-	Create plots of the data and see if there’s any abnormal in the dataset and summarize any pattern observed from the data by hourl/weekday/month
#### Hint:
- try to show smart/efficient way to merge and sum column
-	try not to hard code by column number or name but making the script re-usable for general data formatting

## Assignment 3: EDA and forecast model
#### Objective: create EDA and forecast model to predict RTLMP
We need to analyze and create predictive modeling in daily basis as quantitive analyst. Create EDA using the data and make your model to predict RTLMP from the data.
#### Data Files:
In the data file **timeseries_data.xlsx**, you can find following timeseries (hourly):
-	RTLoad: ERCOT real-time hourly actual load
-	WIND_RTI: ERCOT real-time hourly wind generation
-	GENERATION_SOLAR_RT: ERCOT real-time solar generation
-	RTLMP: ERCOT North hub real-time price
#### Requirements:
-	Create Exploratory Data Analysis (EDA)
- Create forecast model to predict RTLMP
#### Hint:
-	notice the timestamps between independent and explanatory variables 

## Assignment 4 (Optional): Learn products of Futures
#### Objective: self-learning of market products and create hedging method
This assignment will give some information to guide you to learn U.S. Power Futures market products. The goal is to demonstrate self-learning skill and passion to explore/learn new market/products.
#### Products:
- Product 1: Power Futures - ERN
https://www.theice.com/products/6590337/ERCOT-North-345KV-Real-Time-Peak-Fixed-Price-Future
- Product 2: Natural Gas Futures - H
https://www.theice.com/products/6590258/Henry-LD1-Fixed-Price-Future
- Product 3: Heat Rate Futures - XPR
https://www.theice.com/products/27998706/ERCOT-North-345KV-Physical-HR-Peak-HE-0700-2200-Future
#### Data Files:
- **dataset.xlsx**  the file provides the time series of daily settlement prices for same strip (December 2016 product).
#### Requirements:
- create understanding of the products from the links provided. (do more research with uncleared concepts)
- assume Product 1 has no liquidation in the market and we are holding the physical power (same settlement as Product 1), how to use Product 2 & 3 to hedge our exposure to physical power (again, same settlement as Product 1)? 
 - create Excel file model with weekly rebalance of your positions (only rebalance Product 2) to try to achieve hedging. within the Excel file, use parameter to decide your rebalance and summarize the efficiency of hedging.
#### Hint:
- make your own assumptions and explain in summary report
- notice contract size limit


