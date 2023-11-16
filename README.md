# Lake Michigan Sailing Passage Conditions Analysis 2018-2022

## Table of Contents
1. [Introduction](README.md#Introduction)
2. [Data Task](README.md#Data-Task)
3. [Data Processing](README.md#Data-Processing)
4. [Data Cleaning and Manipulation](README.md#Data-Cleaning-and-Manipulation)
5. [Analysis and Visualizations](README.md#Analysis-and-Visualizations)
6. [Summary and Recommendations](README.md#Summary-and-Recommendations)


## Introduction

The following is a case study analyzing weather buoy data provided by NOAA, to determine the best time to make a sailing passage on Lake Michigan from Chicago, IL to Mackinac Island, MI. The data in this project looks at NOAA data that was pulled from 2018-2022 from two separate weather buoys. The south buoy (no. 45007) is located in the open water at the south end of Lake Michigan, approximately 43 nautical miles east-southeast of Milwaukee, WI. The north buoy (no. 45002) is located in the open water at the north end of Lake Michigan, approximately halfway between North Manitou Island, MI, and Washington Island, WI. There are no open water buoys located in the middle portion of Lake Michigan, so the two buoy data sets were analyzed to predict the best time to make a passage based on wind direction, wave height, wind speed, occurrences of small craft advisories, and temperature. 

![Sailing_Passage_Course](/Images/LM_course.jpg)

## Data Task

The goal of this project is to identify when is the most opportune time to make a sailing passage from Chicago, IL to Mackinac Island, MI. Since the boat will be powered by sails, certain considerations need to be made before planning a multi-day open-water sail. 

### Primary Considerations

#### Wind Speed
First and foremost, the number one consideration is that there needs to be wind. Little or no  wind at all, makes for a very slow, boring, and overall unenjoyable sailing trip. Typically, ideal wind conditions that power the boat well but are still comfortable to manage, fall between 10-14 knots. This is a subjective measurement but for this project, we will call 10-14 knots ideal wind conditions. 

#### Wind Direction
The second consideration that needs to be taken into account is wind direction. The physics of sailing does not allow for a sailboat to travel directly into the wind, and based on where the wind is crossing over the boat, dictates where the sails need to be positioned, the degree of heel the boat experiences, and the overall boat speed. The fastest and most comfortable point of sail is called a "beam reach" and this occurs when the boat is traveling perpendicular to the wind direction. The bearing for the sailing route from Chicago, IL to Mackinac Island, MI is primarily NNE (0°-45°), so the ideal wind direction for this trip would need to be coming out of the ESE (90°-130°) or from the WNW (270°-310°.) The worst wind direction for the trip would be the direct point of travel which is primarily NNE (0°-45°.)

![Points of Sail](/Images/POS.jpg)

#### Wave Height
To safely make an open water passage, wave height also needs to be accounted for. If wave heights become too high and occur in short wave periods, sailing in such conditions can become very dangerous to the safety of the crew aboard. For sailing comfort and safety reasons, we will define ideal wave height as <=3ft.

## Data Processing

#### Raw Data
The raw data was downloaded from NOAA's National Buoy Data Center from the following sources:

[North Lake Michigan Buoy No. 45002](https://www.ncei.noaa.gov/access/marine-environmental-buoy-database/45002.html)

[South Lake Michigan Buoy No. 45007](https://www.ncei.noaa.gov/access/marine-environmental-buoy-database/45007.html)

#### Data Licensing
All NOAA data from the National Buoy Data Center is unlicensed and public domain.

#### Data Organization
Once the raw data was downloaded, I renamed the data files with a naming convention based on the different buoys. "N_LM" was used to denote the north buoy no. 45002, and "S_LM" was used to denote the south buoy no. 45007. All files were then stored locally on my computer to begin cleaning and manipulating the data.

#### Issues with the Data
The dates of the data fields pulled from these buoys typically ran from May through November/December, depending on when the buoy was installed and removed that season. The sailing season on the Great Lakes is realistically May-October so these were the months that were focussed on during the analysis stage of the project. However, after initially reviewing the raw data, I encountered two main issues.

1. For the years 2020 and 2021, data was missing for May. Due to the COVID-19 pandemic, buoys those years were installed later than normal and that data is missing. Averages that are calculated for May in this project, for this reason, are 3-year averages versus the standard 5-year averages for the rest of the months in the range. 

2. Many of the fields in the original raw data were listed as "99" or "999" in situations where the readings seemed inaccurate. To verify the data integrity, I reached out to a representative from the National Buoy Data Center to verify the readings. After a follow-up with NOAA, it was confirmed that readings of "99" or "999" were situations where the data was not recorded or there was a technical error with the buoy. In these situations (which occurred inconsistently across all categories) the data fields were replaced with a "null" value. 

## Data Cleaning and Manipulation

To clean the data, I used Microsoft Excel and logged all my changes in a [Changelog.](https://github.com/franc136/Lake-Michigan-Sailing-Passage-Conditions-Analysis-2018-2022/blob/main/NOAA_buoy_data_project_CHANGELOG.csv)

Major data changes that were applied to all 10 data files:

1. The columns "_yr", "mo", and "dy" were concatenated to form one "Date" column.
2. The columns "hr" and "mn" were concatenated to form one "Time" column.
3. Searched readings listed as "99" or "999" and replaced them with "null" based on NOAA representative data integrity confirmation. 
4. The row labels "WDIR" and "DegT" were combined into a single column label, "W_DIR_degT".
5. A new column "W_SPD_knts" was created, and the wind speed was converted from m/s into knots by multiplying the m/s value by 1.944.
6. A new column "Wv_HT_ft" was created, and the wave height was converted from meters to feet by multiplying the m value by 3.281.
7. The column title "DPD" was changed to "Dom_wv_pd_sec". 
8. The column title "APD" was changed to "Avg_wv_pd_sec".
9. The column title "MPD" was changed to "Wv_DIR_degT". 
10. The data row labels "PRES" and "hpa" were combined to create a new column label "PRES_hPa".
11. The column "Air_Temp_degF" was created, and the degrees Celcius values were converted into degrees Fahrenheit by multiplying the DegC value by 1.8, then adding 32. 
12. The column "Wtr_Temp_degF" was created, and the degrees Celcius values were converted into Fahrenheit by multiplying the DegC value by 1.8, then adding 32.
13. The column "Dew_pt_degF" was created, and the degree Celcius values were converted into Fahrenheit by multiplying the DegC value by 1.8, then adding 32. 
14. The data row labels "Vis" and "mi" were combined to rename and create the column "Vis_mi".
15. The data row labels "TIDE" and "ft" were combined to rename and create the column "TIDE_ft".

## Analysis and Visualizations

Once the 10 data files for the North and South buoys were cleaned, I created two combined (2018-2022) .csv files for each buoy's data and uploaded the files into BigQuery. 

All analysis was performed in SQL, and the queries used in this case study can be reviewed [here.]( https://github.com/franc136/Lake-Michigan-Sailing-Passage-Conditions-Analysis-2018-2022/blob/main/NOAA_buoy_data_SQLqueries)

All visualizations were created in Tableau Public and the interactive dashboards can be explored and accessed [here.](https://public.tableau.com/app/profile/sean.francis6127/viz/LakeMichiganSailingPassage-ConditionsAnalysis2018-2022/Story1#1)

### Atmosphere and Lake Conditions 
To begin my analysis, I first looked at the general atmospheric conditions of the lake, along with surface conditions such as average wind speeds and wave heights. To define the weather conditions, each category represents a range of barometric pressures (hPa). The ranges come from displays typically used on a barometer face. Ranges as follows:

Very Dry Weather (1049.8 - 1066.7 hPa)

Fair Weather (1022.7 - 1049.8 hPa)

Changing to Fair Weather (1015.9 -1022.7 hPa)

Changing to Poor Weather (1009.1 - 1015.9 hPa)

Poor/Rainy Weather (982.1 - 1009.1 hPa)

Stormy Weather (965.1 - 982.1 hPa)

A Small Craft Advisory is another indicator that was used to track conditions on the lake. A Small Craft Advisory is a weather warning broadcast by NOAA as a part of their marine forecast when wind conditions are in the 20-33knt range or wave heights are >4ft.

#### South Buoy No. 45007

![South Buoy Visualizations](/Images/S_Atmo.png)

###### Weather Conditions
In the south of the lake, October had the most hours of "Fair" weather with an average of 86.8 hours, but September had more total hours of "Fair" and "Changing to Fair" weather, with a combined average of 332.9 hours. October had the most average hours of "Poor/Rainy" weather, but August had more total hours of "Poor/Rainy" and "Changing to Poor" weather, with a combined average of 346.1 hours.

Temperature-wise, August had the highest average temperature at 72.6 °F and May had the lowest at 50.7 °F.

###### Surface Conditions
October experienced the highest average wind speeds at 14.1 knots, as well as the highest average wave height of 3.9ft. 
May saw the lowest average wind speed at 7.8 knots, while July had the lowest average wave height of 1.4ft.

###### Small Craft Advisories
October experienced the most SCA's with an average of 20.4, while May had the lowest amount with an average of 1.7.

#### North Buoy No. 45002

![North Buoy Visualizations](/Images/N_Atmo.png)
###### Weather Conditions
In the north of the lake, once again, October had the most hours of "Fair" weather with an average of 134.8 hours, but September had more total hours of "Fair" and "Changing to Fair" weather, with a combined average of 389.8 hours. October also had the most average hours of "Poor/Rainy" weather, but June had more total hours of "Poor/Rainy" and "Changing to Poor" weather, with a combined average of 464.8 hours.

Temperature-wise, August had the highest average temperature at 68.5 °F and May had the lowest at 42.5 °F.

###### Surface Conditions
October experienced the highest average wind speeds at 14.2 knots, as well as the highest average wave height of 3.9ft.
May saw the lowest average wind speed at 7.6 knots, while July had the lowest average wave height of 1.4ft.

###### Small Craft Advisories
October experienced the most SCA's with an average of 18.4, while May had the lowest amount with an average of 3.5.


### Wind Conditions
Next, I analyzed different wind conditions including, average hours of ideal sailing conditions, average hours of ideal wind directions, and average hours of worst possible wind direction. To define ideal sailing conditions, wind speed had to be between 10-14 knots and wave height had to be <=3ft. 

#### South Buoy No. 45007

![South Buoy Visualizations](/Images/S_Wind.png)

###### Ideal Sailing Conditions
In the south of the lake, August had the highest average amount of days where ideal conditions occurred, but September had the highest average of hours of ideal sailing conditions, at 26.8 hours/month. 

###### Wind Direction
October saw the highest average hours of ideal wind direction with 57.4 hours/month out of the (ESE) and 70.1 hours/month out of the (WNW). July experienced the lowest average hours of ideal wind direction out of the (ESE) with 24.1 hours/month, while May experienced the lowest ideal wind direction out of the (WNW) with 28.1 hours/month.

Looking at conditions with the worst possible wind direction for the trip, July had the highest average hours of winds out of the (NNE) at 96.8 hours/month, while May had the lowest average hours at 45.3 hours/month. 

#### North Buoy No. 45002

![North Buoy Visualizations](/Images/N_Wind.png)

###### Ideal Sailing Conditions
In the north of the lake, August had the highest average amount of days where ideal conditions occurred at 26.6 days/month, as well as the highest average of hours of ideal sailing conditions at 28.1 hours/month. 

###### Wind Direction
May saw the highest average hours of ideal wind direction at 54 hours/month out of the (ESE), while October had the highest average hours of ideal wind direction at 91.9 hours/month out of the (WNW). July experienced the lowest average hours of ideal wind direction out of the (ESE) with 23.9 hours/month, while May experienced the lowest ideal wind direction out of the (WNW) with 29.3 hours/month.

Looking at conditions with the worst possible wind direction for the trip, August had the highest average hours of winds out of the (NNE) at 122.2 hours/month, while October had the lowest average hours at 80.9 hours/month. 

## Summary and Recommendations

After considering all conditions for both buoys, September consistently ranked highly for the majority of categories and proved to be the best month for the passage.

1. September was the only month where average wind speeds and wave height fell within the ideal conditions (10-14knt wind speed, <=3ft) for both buoys.
2. September had the highest combined average hours of "Fair" and "Changing to Fair" weather conditions for both buoys.
3. September had an average air temperature above 60 °F for both buoys, which makes for very comfortable sailing weather.
4. September ranked first and third for the highest average days/month where ideal sailing conditions occurred and hours/month of ideal sailing conditions.
5. September ranked second and third highest for average hours/month of ideal wind direction conditions for both buoys.
6. September randed second and third lowest in days/month of worst wind direction conditions for both buoys.

The only issue with September is that it ranked second for most Small Craft Advisories/month for both buoys. 

### September Weekly Conditions Summary

To take the analysis one step further, once September was identified as the most ideal month for the passage, I analyzed ideal and worst wind direction conditions as well as ideal and worst weather conditions by month. 

![September Weekly Conditions](/Images/Sept_Smry.png)

### Passage Recommendations

After reviewing the conditions by week, I would recommend that the best time for a passage from Chicago, IL to Mackinac Island, MI would be during the second week of September (9/8-9/14.)

1. The second week had the most consistent average hours of ideal wind direction conditions.
2. The second week had average hours of "Fair" weather ranging from high to average, compared to the other weeks.
3. The second week had below-average hours of "Poor/Rainy" weather.

The only issue the second week may encounter is the possibility of above-average hours of (NNE) wind direction conditions on the north end of the passage, but for the reasons highlighted above, I would still recommend the second week as an overall recommendation.
