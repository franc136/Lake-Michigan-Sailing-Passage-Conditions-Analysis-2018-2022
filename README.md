# Lake Michigan Sailing Passage Conditions Analysis 2018-2022

## Table of Contents
1. [Introduction](Readme.md#Introduction)
2. [Data Task](Readme.md#Data-Task)
3. [Data Processing](Readme.md#Data-Processing)
4. [Data Cleaning and Manipulation](Readme.md#Data-Cleaning-and-Manipulation)
5. [Analysis and Visualizations](Readme.md#Analysis-and-Visualizations)
6. [Summary and Recommendations](Readm.md#Summary-and-Recommendations)


## Introduction

The following is a case study analyzing weather buoy data provided by NOAA, to determine the best time to make a sailing passage on Lake Michigan from Chicago, IL to Mackinac Island, MI. The data in this project looks at NOAA data that was pulled from 2018-2022 from two separate weather buoys. The south buoy (no. 45007) is located in the open water at the south end of Lake Michigan, approximately 43 nautical miles east-southeast of Milwaukee, WI. The north buoy (no. 45002) is located in the open water at the north end of Lake Michigan, approximately halfway between North Manitou Island, MI, and Washington Island, WI. There are no open water buoys located in the middle portion of Lake Michigan, so the two buoy data sets were analyzed to predict the best time to make a passage based on wind direction, wave height, wind speed, occurrences of small craft advisories, and temperature. 

![Sailing_Passage_Course](/Images/LM_course.jpg)

## Data Task

The goal of this project is to identify when is the most opportune time to make a sailing passage from Chicago, IL to Mackinac Island, MI. Since the boat will be primarily powered by sail, certain considerations need to be made before planning a multi-day open-water sail. 

### Primary Considerations

#### Wind Speed
First and foremost, the number one consideration is that there needs to be wind. Little or no  wind at all, makes for a very slow, boring, and overall unenjoyable sailing trip. Typically, ideal wind conditions that power the boat well but are still comfortable to manage, fall between 10-14 knots. This is a subjective measurement but for this project, we will call 10-14knts ideal wind conditions. 

#### Wind Direction
The second consideration that needs to be taken into account is wind direction. The physics of sailing does not allow for a sailboat to travel directly into the wind, and based on where the wind is crossing over the boat, dictates where the sails need to be positioned, the degree of heel the boat experiences, and the overall boat speed. The fastest and most comfortable point of sail is called a "beam reach" and this occurs when the boat is traveling perpendicular to the wind direction. The bearing for the sailing route from Chicago, IL to Mackinac Island, MI is primarily NNE(0°-45°), so the ideal wind direction for this trip would need to be coming out of the ESE(90°-130°) or from the WNW(270°-310°.) The worst wind direction for the trip would be the direct point of travel which is primarily NNE(0°-45°.)

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



## Data Cleaning and Manipulation

## Analysis and Visualizations

## Summary and Recommendations
