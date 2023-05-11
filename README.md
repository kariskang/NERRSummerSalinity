# NERR Summer Salinity

A repo for Karis Kang's final project for BIO539 Spring 2023

## Purpose:

- To determine historical salinity trends during the summer (May through Aug) at three coastal field sites over the past 26 years (1996 - 2021)

## Abstract

Sea-level rise (SLR) in the northeast Atlantic is roughly 3-4 times greater than the global average and significantly higher than on the Pacific and Gulf coasts. As a result, New England saltmarshes face increased environmental stress from flooding and salinity as SLR outpaces sediment accretion. In an effort to determine whether different saltmarsh plant populations differ in stress response to SLR, I'm planning to conduct a common garden study in which several populations of three saltmarsh plant species are exposed to a range of salinity values. The following data analysis has been conducted to calculate average monthly salinity from May through Aug (the time period during which the study will be conducted) for three saltmarsh collection sites, as well as average salinity variance over the course of these four months. This information will be used to establish a range of appropriate salinity treatments for this experiment. 

## Data

All water quality data is taken from NOAA's System Wide Monitoring Program (SWMP) conducted at the National Estuarine Research Reserves (NERR). Files were downloaded as monthly summary data through the SWMPrats Widget at https://beckmw.shinyapps.io/swmp_summary/ created by Marcus Beck and Todd O'Brien. The SWMP data policy can be found here at https://cdmo.baruch.sc.edu/data/policy.cfm 

Downloaded data for three sites (Wells, ME; Great Bay, NH; Narragansett Bay, RI) were given a site designation before being combined into one csv file with site, month, year, and mean salinity (psu) information. Working document was filtered to exclude all N/A values. Graphs and statistical analyses were performed in Rstudio for all three sites. The results from the Rstudio analyses were then used to test the functionality of a bash script intended to calculate salinity averages and variance from raw water quality csv data downloaded for other monitoring stations in the SWMP system. 

## Languages: 
- R
- Bash Shell

## Files: 

### Data: 
- MonthlySalinity_95-22_Wells_GB_Narg_combined.csv 
  - monthly water quality data from Wells, Great Bay, and Narragansett Bay combined into one file after being downloaded as separate csv files from the SWMP widget 
- SummerSalinity.csv  
  - contains only average monthly salinity data from May-Aug of each year from 1996 - 2021 for Wells, Great Bay, and Narragansett Bay; n/a values filtered out

### Analysis Documentation
- Karis_Final_Project.md  
  - R Markdown document with step-by-step documentation of all R code for analyses and plots generated
  - Plots and figures in .md file having trouble loading on github page, images provided separately in repo: 
   - salplots.png - plot of average summer salinity over time for three sites 
   - tukey.png - tukey plot to show differences in average summer salinity among sites

### Writing: 
- ReadMe 
  - Summary of repo purpose and contents 
- KangFinalPaper 
  - written report of background, methods, data analysis, and findings
