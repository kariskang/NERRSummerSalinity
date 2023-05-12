# Introduction

Sea level rise (SLR) in the Atlantic northeast is roughly 3-4 times the global average and is increasing at a greater rate in the northeast Atlantic than on the Pacific or Gulf coasts (Sallenger et al., 2012; Boon, 2012). In southern New England, SLR has nearly doubled over the past two decades compared to the historic average (Watson et al., 2017) making saltmarshes in southern New England --- typically small area fringe marshes located in estuaries along tidal ponds, tidal rivers, and behind barrier spits (Roman et al., 2000) --- particularly vulnerable to inundation and habitat loss.

Rhode Island populations of high-marsh grasses such as Spartina patens have shrunk in the past decade as rising tides have increased flooding and salinity stress on coastal habitat (Watson et al. 2016). In order to assess the impact of SLR related stressors on saltmarsh plant populations across the region, I am proposing a series of common garden experiments where different populations of saltmarsh grasses are exposed to a range of salinity conditions. It is to determine a baseline for these salinity conditions that I've analyzed historical water quality data at three field sites from 1996 until 2021 to find: 1) mean summer (May-Aug) salinity, 2) summer salinity variance, and 3) whether there are significant differences in mean salinity and salinity variance across time and among sites.

# Methods

## Data Collection:

The [System Wide Monitoring Program](https://cdmo.baruch.sc.edu/about/overview.cfm) (SWMP) collects long-term water quality and meteorological data at NOAA's National Estuarine Research Reserves (NERR), a series of research reserves located along watersheds on the Atlantic, Pacific, and Gulf coasts as well as the Great Lakes. Three reserves in New England have been collecting data since the 1990's: Wells, ME, Great Bay, NH, and Narragansett Bay, RI; Waquoit Bay NERR was excluded from this analysis due to monitoring data that did not span the same years as the other three research stations. Data from these three reserves were downloaded as monthly summary data from the [SWMPrats summary data widget](https://beckmw.shinyapps.io/swmp_summary/) and formatted into a .csv file listing site, month (May-Aug), year (1996-2021), and mean monthly salinity (psu); only summer months were used in this analysis due potential future experiments being run during the summer field season. Formatted data was then uploaded to the project github repository as SummerSalinity.csv.

## R Analysis:

Salinity data was downloaded from the project's github repository [here](https://raw.githubusercontent.com/kariskang/NERRSummerSalinity/main/SummerSalinity.csv) and read into a Rmd file. Dplyr was used to summarize data and find averages and variances for monthly summer salinity across years and research reserves (referred to as Sites within the document). Differences in average summer salinity across 1) research reserves (Sites), and 2) years for each research reserve (Sites x years) were calculated using R's ANOVA function (𝛂 = 0.05) and followed with a post-hoc Tukey test to determine which groups were significantly different. Average summer salinity for each year was plotted using ggplot for all three research reserves.

# Results

Average summer salinity was different across research reserves (f = 1274.845, p \< 0.0001) but not across years when research reserve (site) was taken into account (f = 1.093, p = 0.33647). Post-hoc analysis showed all research reserves to have different average summer salinities, with Well, ME exhibiting the greatest difference.

**Table 1.**  *Summary data for monthly salinity averages and variance for three New England research reserves, as calculated from reported mean monthly salinity from May - Aug during the years 1996-2021*

| **Site**             | **Avg Summer Salinity (x)** | **Avg Summer Salinity Variance (σ2**) | **Number of monthly averages (n)** |
|----------------------|-----------------------------|---------------------------------------|------------------------------------|
| Narragansett Bay, RI | 28.5                        | 2.12                                  | 104                                |
| Great Bay, NH        | 23.6                        | 24.6                                  | 90                                 |
| Wells, ME            | 4.12                        | 16.1                                  | 104                                |

**Table 2.** *ANOVA and results when looking at differences in average summer salinity per site and per year x site*

+----------------+--------+------------+-------------+-------------+-------------+
|                | **Df** | **Sum Sq** | **Mean Sq** | **F-value** | **P-value** |
+================+========+============+=============+=============+=============+
| **Site**       | 2      | 34154      | 17077       | 1274.845    | \< 2e-16    |
+----------------+--------+------------+-------------+-------------+-------------+
| **Year**       | 1      | 134        | 134         | 10.002      | 0.00173     |
+----------------+--------+------------+-------------+-------------+-------------+
| **Site\*Year** | 2      | 29         | 15          | 1.093       | 0.33647     |
+----------------+--------+------------+-------------+-------------+-------------+
| **Residuals**  | 292    | 3911       | 13          | \           | \           |
+----------------+--------+------------+-------------+-------------+-------------+

**Table 3.** *Post-hoc Tukey multiple comparisons of average summer salinity values among sites*

|                        | **Diff**   | **Lower**  | **Upper**   | **P-Adj** |
|------------------------|------------|------------|-------------|-----------|
| Narragansett-Great Bay | 4.906148   | 3.664885   | 6.14741     | \<0.01    |
| Wells-Great Bay        | -19.444753 | -20.686015 | -18.20349   | \<0.01    |
| Wells-Narragansett     | -24.350900 | -25.546537 | -23.15526   | \<0.01    |

![**Figure 1.** *Wells, ME showed the greatest difference in average summer salinity among the three sites, though salinity differences among all sites were significant*](Karis_Final_Project_files/figure-gfm/tukey-1.png)

![**Figure 2.** *Average summer salinity at New England coastal research stations has not changed significantly overall over the past 26 years (ANOVA, Factor = Site x Year, f = 1.093, p =0.33647, α = 0.05). However, average summer salinity is different among research stations (ANOVA, Factor = Site, f = 1274.845, p \< 2e-16, α = 0.05).*](salplots-1.png)

## **Discussion**

Although there were significant differences in average summer salinity among years when data from all three research stations were lumped together, these differences disappear when salinity values are grouped together by location, suggesting that overall coastal salinity has not changed over the past quarter century at these research stations, though dramatic fluctuations might happen from year to year. However, there are consistent differences in salinity concentrations among research station sites, with Wells, ME having experienced an average salinity of 4.12 psu over the summer months while Narragansett Bay, RI records an average salinity of 28.5 psu over the 26 year time-frame. 

Although the general trend seems to be that average summer salinity is higher at low latitudes, and lower at high latitudes, this does not seem to be consistent with the geographic distances between research stations used in this analysis; Tukey's test showed Wells to have the greatest differences in mean among research stations, yet it is only \~38 km from Great Bay, and \~200 km from Narragansett Bay. Meanwhile Narragansett and Great Bay, while significantly different, were closer together in salinity values and are \~ 167 km apart.

**Table 4.** *Location data for the three research stations where water quality data was collected from; straight-line distances between research stations measured via Google Maps by the graduate student* 

| Location             | Latitude  | Approximate straight-line distance from neighboring research stations |
|----------------------|-----------|-----------------------------------------------------------------------|
| Narragansett Bay, RI | 41.64055  | Great Bay (\~167 km); Wells (\~200 km)                                |
| Great Bay, NH        | 43.0722   | Wells (\~38 km); Narragansett (\~167 km)                              |
| Wells, ME            | 43.298347 | Great Bay (\~38 km); Narragansett (\~200 km)                          |

Overall the pattern of the data suggests that different saltmarsh sites in the New England region are exposed to different levels of salinity concentration over the growing season and that those salinity conditions have not changed significantly over time as measured by summer averages. Furthermore, these differences may follow a roughly latitudinal gradient, and the relationship between latitude and coastal salinity should be further explored using data collected from a larger range of research stations along the Atlantic coast. Although not statistically analyzed in this report, differences in within-season and year-to-year variation for salinity concentrations may also be present among sites and bears further study. 

## **Conclusion**

Although sea-level rise exposes saltmarsh grasses to increased salinity stress through prolonged submergence time, regional differences in the salinity of coastal waters during the growing season could mean some populations of saltmarsh grasses are better adapted to high salinity concentrations than others. As such, garden experiments testing differences in local adaptation among salmarsh populations should reference the long-term salinity trends of their collection sites when choosing environmental parameters for their design. Future analyses of SWMP monitoring data should not only compare average salinity values across sites, but also seasonal salinity variance and any geographic patterns in salinity data when assessing potential selective pressures influencing SLR resilience of New England saltmarshes. 

## **Acknowledgements**

I would like to thank Dr. Daisy Durant and Dr. Kenneth Raposa at the Narragansett Bay NERR for their mentorship and willingness to familiarize me with both field collection and data formatting protocols for SWMP's long-term environmental datasets, as well as my classmates and Dr. Rachel Schwartz for their patience and assistance as I grappled with coding languages for the first time this semester. 

## **Literature Cited**

Boon, J. D. (2012). Evidence of sea level acceleration at US and Canadian tide stations, Atlantic Coast, North America. Journal of Coastal Research, 28(6), 1437-1445.

NOAA National Estuarine Research Reserve System (NERRS). System-wide Monitoring Program. Data accessed from the NOAA NERRS Centralized Data Management Office website:<http://www.nerrsdata.org>; accessed 20 April 2023

Raposa, K. B., Cole Ekberg, M. L., Burdick, D. M., Ernst, N. T., & Adamowicz, S. C. (2017). Elevation change and the vulnerability of Rhode Island (USA) salt marshes to sea-level rise. Regional Environmental Change, 17(2), 389-397.

Sallenger Jr, A. H., Doran, K. S., & Howd, P. A. (2012). Hotspot of accelerated sea-level rise on the Atlantic coast of North America. Nature Climate Change, 2(12), 884-888.

Watson, E. B., Raposa, K. B., Carey, J. C., Wigand, C., & Warren, R. S. (2017). Anthropocene survival of southern New England's salt marshes. Estuaries and Coasts, 40, 617-625.

Watson, E. B., Szura, K., Wigand, C., Raposa, K. B., Blount, K., & Cencer, M. (2016). Sea level rise, drought and the decline of Spartina patens in New England marshes. Biological Conservation, 196, 173-181.
