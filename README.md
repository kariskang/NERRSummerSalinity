# NERRSummerSalinity
A repo for Karis Kang's final project for BIO539 Spring 2023

## Purpose: 
- To determine historical salinty trends during the summer (May through Aug) at three coastal field sites over the past 26 years (1996 - 2021)
- To create scripts which will give summary data on summer salinity for any future SWMP datasets

## Abstract
Sea-level rise (SLR) in the northeast Atlantic is roughly 3-4 times greater than the global average and significantly than SLR on the Pacific and Gulf coasts. As a result, New England saltmarshes cannot accumulate sediment at a rate which outpaces SLR and are facing increased environmental stress from flooding and salinity. In an effort to determine whether different saltmarsh plant populations differ in stress response to SLR, I'm planning to conduct a commmon garden study in which different populations of several saltmarsh plant species are exposed to a range of salinity values. The following data analysis has been conducted to calculate average monthly salinity for three saltmarsh sites from May through Aug (the time period during which the study will be conducted) as well as average salinity variance over the course of these four months; these values will be calculated using long-term monitoring data collected from 1996 to 2021, made publically available through NOAA and the National Estuarine Research Reserves.

## Data
All water quality data is taken from NOAA's System Wide Monitoring Program (SWMP) at the National Estuarine Research Reserves. Files were downloaded as monthly summary data through the SWMPrats Widget at https://beckmw.shinyapps.io/swmp_summary/ created by Marcus Beck and Todd O'Brien. Downloaded data were given site designation before being combined into one csv file with site, month, year, and mean salinity (psu). Working document was filtered to exclude all NA values.

