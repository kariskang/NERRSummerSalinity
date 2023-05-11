RStudio Codespace for NERR Salinity Analysis
================

## Project Goals:

-   Using monthly summarized water quality data from May to Aug (1996
    -2021) collected from three sites, find:

    -   average summer salinity
    -   average summer salinity variance

-   Determine if differences are significant among:

    -   Sites
    -   Years
    -   Years x Sites

-   Plot yearly summer salinity across years for all sites

## Import Libraries

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.6     ✓ dplyr   1.0.8
    ## ✓ tidyr   1.2.0     ✓ stringr 1.4.0
    ## ✓ readr   2.1.2     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

## Import Formatted Salinity Data

``` r
# import data from https://raw.githubusercontent.com/kariskang/NERRSummerSalinity/main/SummerSalinity.csv 
SummerSalinity <- read.csv('https://tinyurl.com/msaejryj') 
```

## Summary Data for Dataset

``` r
# check sample size for each site to make sure they're comparable
SummerSalinity %>% 
    group_by(Site) %>% 
    summarize(DataPtCount_Site = n())
```

    ## # A tibble: 3 × 2
    ##   Site         DataPtCount_Site
    ##   <chr>                   <int>
    ## 1 Great Bay                  90
    ## 2 Narragansett              104
    ## 3 Wells                     104

## Find average summer salinity and variance for each site across all years

``` r
# check mean summer salinity and mean summer salinity variance across all years for each site
SummerSalinity %>% 
  group_by(Site) %>% 
  summarize(AvgSal = mean(mean_salinity), 
            AvgVar = var(mean_salinity))
```

    ## # A tibble: 3 × 3
    ##   Site         AvgSal AvgVar
    ##   <chr>         <dbl>  <dbl>
    ## 1 Great Bay     23.6   24.6 
    ## 2 Narragansett  28.5    2.12
    ## 3 Wells          4.12  16.1

## Statistical Analysis using ANOVA

``` r
# I want the differences among sites across all years, and difference among years grouped by site (interaction of Site x Year)
ANOVASitesYears <- aov(mean_salinity ~ Site*year, data = SummerSalinity)
#summary of ANOVA results
summary(ANOVASitesYears)
```

    ##              Df Sum Sq Mean Sq  F value  Pr(>F)    
    ## Site          2  34154   17077 1274.845 < 2e-16 ***
    ## year          1    134     134   10.002 0.00173 ** 
    ## Site:year     2     29      15    1.093 0.33647    
    ## Residuals   292   3911      13                     
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

There is a significant difference (*α* = 0.05) in mean summer salinity
among sites (f = 1274.845, p \< 2e-16) and among years when looking at
all sites grouped together (f = 10.002, p = 0.00173), but not among
years when each site is taken into account separately (f = 1.093, p =
0.33647)

## Post-hoc Tukey test to determine significance in salinity differences among sites

``` r
#I want to know which groups in Sites are significant from the others, and by how much

#Running a Tukey test; thank you statology.org for my life
TukeyHSD(ANOVASitesYears, 'Site', conf.level=.95) 
```

    ## Warning in replications(paste("~", xx), data = mf): non-factors ignored: year

    ## Warning in replications(paste("~", xx), data = mf): non-factors ignored: Site,
    ## year

    ##   Tukey multiple comparisons of means
    ##     95% family-wise confidence level
    ## 
    ## Fit: aov(formula = mean_salinity ~ Site * year, data = SummerSalinity)
    ## 
    ## $Site
    ##                              diff        lwr       upr p adj
    ## Narragansett-Great Bay   4.906148   3.664885   6.14741     0
    ## Wells-Great Bay        -19.444753 -20.686015 -18.20349     0
    ## Wells-Narragansett     -24.350900 -25.546537 -23.15526     0

``` r
#Plotting Tukey test results
plot(TukeyHSD(ANOVASitesYears, 'Site'))
```

    ## Warning in replications(paste("~", xx), data = mf): non-factors ignored: year

    ## Warning in replications(paste("~", xx), data = mf): non-factors ignored: Site,
    ## year

![](R-Salinity-Analysis-Documentation_files/figure-gfm/tukey-1.png)<!-- -->

Average summer salinity is significantly different among all three
sites. Wells, ME has the largest negative difference from Narragansett
Bay and Great Bay despite the fact that Great Bay, NH, and Wells, ME are
closer geographically (\~39 km) than Great Bay NH, and Narragansett Bay,
RI (\~167 km).

## Plot mean summer salinity across years for each site

``` r
# average mean salinity values from May to Aug so there's one summer salinity value for each year
yearlysummersal <- SummerSalinity %>% 
  group_by(Site, year) %>% 
  summarize(yearlysummersal = mean(mean_salinity))
```

    ## `summarise()` has grouped output by 'Site'. You can override using the
    ## `.groups` argument.

``` r
# went back and created a labels variable so site order in the legend would match the order on the graph
labels <- yearlysummersal %>% filter(year == 2021) %>% 
  arrange(desc(yearlysummersal)) %>% pull(Site)

# plot average yearly summer salinity across years for each site 
ggplot(yearlysummersal, aes(year, yearlysummersal, color = Site)) +
  geom_line() +
  labs(x = "Year", y = "Mean Summer Salinity (psu)", color = "") +
  theme_bw() + 
  scale_color_discrete(breaks = labels, labels = labels) 
```

![](R-Salinity-Analysis-Documentation_files/figure-gfm/salplots-1.png)<!-- -->

**Figure 1.** Average summer salinity at New England coastal research
stations has not changed significantly overall over the past 26 years
(ANOVA, Factor = Site x Year, f = 1.093, p =0.33647, *α* = 0.05).
However, average summer salinity is different among research stations
(ANOVA, Factor = Site, f = 1274.845, p \< 2e-16, *α* = 0.05), with lower
average summer salinity values at higher latitudes (Narragansett Bay,
RI: 41.64055, Great Bay, NH: 43.0722, Wells, ME: 43.298347).
