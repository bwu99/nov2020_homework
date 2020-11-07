## Introduction
This is for Guzman Energy November 2020 Full-Time Internship recuriting process. 
- All assignments are optional. You can choose some or all to do. Both effort and result will be used for final evaluation.
- You can use either R or Python (Recommended) for coding.
- Requirement:
  - create your own github repository for result delivery
  - pdf summary report for each assignment is recommended
  - if you choose python, create jupyter notebook file
  - all code shall no bug runnable by simply cloning to local folder
- **Due: before November 23rd, 2020 5pm ET**

## Assignment 1: Power Calendar function
#### Objective: write R/Python function giving number of hours by iso/peak.type/period
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
#### Objective: merge different data source into single dataset and evaluate the dataset for anormaly (if any)
For analysis purpose, we always have different data sources to merge and format. It’s important to understand the data and format it correctly. 
#### data files:
-	**USA_AL_Auburn-Opelika.AP.722284_TMY3_BASE.csv**
  This file gives hourly electricity consumptions for a resident with unit in kw (kilowatt). 
-	**new.app4.csv**
  Assuming this is one appliance’s electricity consumption minute by minute which is not captured in the previous file. 
  The unit in the file is in watt.
#### Requirements:
-	**for R, use R dplyr package; for Python, use dfply package**
- Create script to load both files. 
-	Given the limitation of data period, try to find the overlap period and merge the data into hourly. (ignore the year but making sure the date/hour matched)
-	After merging the source files correctly, please create one more column in the output file to give total hourly consumption of electricity. (sum all columns)
-	try to plot the data and see if there’s any abnormal in the dataset and summarize any pattern observed from the data by hourl/weekday/month
#### Hint:
- try to show smart/efficient way to merge and sum column
-	try not to hard code by column number or name but making the script re-usable for general data formatting

## Assignment 3: EDA and forecast model
#### Objective: create EDA and forecast model to predict RTLMP
In the data file (timeseries_data.xlsx), you can find following timeseries (hourly):
-	RTLoad: ERCOT real-time hourly actual load
-	WIND_RTI: ERCOT real-time hourly wind generation
-	GENERATION_SOLAR_RT: ERCOT real-time solar generation
-	RTLMP: ERCOT North hub real-time price
#### Requirements:
-	Create Exploratory Data Analysis (EDA)
- Create forecast model 
Hints:
-	Plots/statistics by month/weekday/HE/peak_type
-	Use package ggplot2


