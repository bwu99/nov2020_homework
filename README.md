## Introduction
This is for Guzman Energy November 2020 Full-Time Internship recuriting process. 
- All assignments are optional. You can choose some or all to do. Both effort and result will be used for final evaluation.
- You can use either R or Python for coding.
- Requirement:
  - create your own priviate github repository for result delivery
  - create readme for each assignment under individual folder
  - if you choose python, create jupyter notebook file
  - all code shall no bug runnable by simply cloning to local folder
- Due: before November 23rd 5pm ET 

## Assignment 1: Power Calendar function
#### Objective: write R/Python function giving number of hours by iso/peak.type/period
In power market, the industry defines certain hour of each day to peak type for block trading, so we need to calculate correctly how many hours belongs to certain block. Each ISO has a little different definition of it. 
- See reference: https://www.energygps.com/HomeTools/PowerCalendar

#### Function: get.hours(iso, peak.type, period)
#### Params: (all params are required in the function)
-	iso (character): one of PJM/MISO/ERCOT/SPP/NYISO/WECC/CAISO (see item 1 below)
-	peak.type (character): one of onpeak/offpeak/flat/2x16H/7x8
-	period (character): has 4 types: “2018-2-3” as a daily, “2018Mar” as a monthly, “2018Q2” as a quarterly, “2018A” as an annually.
#### Return:  a list variable giving iso/peak.type/start.date/end.date/num.hour where num.hour is the total number of hours of that peak type in that period.
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


## Assignment 2

## Assignment 3
