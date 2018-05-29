Geospatial analysis
================

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 3.4.2

    ## ── Attaching packages ────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
    ## ✔ tibble  1.4.1     ✔ dplyr   0.7.4
    ## ✔ tidyr   0.7.2     ✔ stringr 1.2.0
    ## ✔ readr   1.1.1     ✔ forcats 0.2.0

    ## Warning: package 'tidyr' was built under R version 3.4.2

    ## Warning: package 'purrr' was built under R version 3.4.2

    ## Warning: package 'dplyr' was built under R version 3.4.2

    ## ── Conflicts ───────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(stringr)
library(dplyr)
library(ggplot2)
library(ggmap) 
setwd("~/Dropbox/HARRIS/Spring 2018/DATA VIZ/geospatial analysis")
```

``` r
stations <- read_csv("Police_Stations.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   x = col_double(),
    ##   y = col_double()
    ## )

``` r
homicides <- read_csv("homicide.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   y = col_double(),
    ##   x = col_double()
    ## )

``` r
sex_assaults <- read_csv("sexual_assault.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   y = col_double(),
    ##   x = col_double()
    ## )

``` r
chicago <- get_map("Chicago")
```

    ## Map from URL : http://maps.googleapis.com/maps/api/staticmap?center=Chicago&zoom=10&size=640x640&scale=2&maptype=terrain&language=en-EN&sensor=false

    ## Information from URL : http://maps.googleapis.com/maps/api/geocode/json?address=Chicago&sensor=false

``` r
ggmap(chicago) + geom_point(data = homicides, mapping = aes(x = x, y = y), col = "red")+ geom_point(data = stations, mapping = aes(x = y, y = x), col = "blue") 
```

![](geospatial_analysis_files/figure-markdown_github/unnamed-chunk-2-1.png)

``` r
ggmap(chicago)  + geom_point(data = sex_assaults, mapping = aes(x = x, y = y), col = "purple")+ geom_point(data = stations, mapping = aes(x = y, y = x), col = "blue")
```

    ## Warning: Removed 1 rows containing missing values (geom_point).

![](geospatial_analysis_files/figure-markdown_github/unnamed-chunk-2-2.png)

Using geospatial data from the City of Chicago on crime in 2018 and police stations locations, along with the function ggmap, I plotted the distribution of police stations in the city with the total number of homicides in 2018 in one graph, and with the total number of sexual assaults in another.

Is it truthful? The data in my plots is truthful because it comes from a reliable source (police stations: <https://data.cityofchicago.org/Public-Safety/Police-Stations/z8bn-74gv>, crime: <https://data.cityofchicago.org/Public-Safety/Crimes-2018/3i3m-jwuy>) and I am plotting the locations of this incidents with the location of police stations in the city as a proxy for “safer” areas.

Is it functional? The plots are functional because they let us see both the amount and location of homicides, sexual assaults and police stations in the city. It is easy to identify each neighborhood by using a map from google maps.

Is it beautiful? I believe the map is beautiful because by using google maps, we can have a very nice map with a lot of detail, and the points are added clearly and in a clean matter.

Is it insightful? I think these plots are insightful because we can see that the homicides are distributed in the most dangerous and less wealthy areas of the city like the south and the west side, and are not influenced by the location of the police stations, contradicting my hypothesis that the location of a police station makes a neighborhood more safe. I think these kind of analysis are useful for policy analysis to see where a stronger security is needed.

Is it enlightening? These maps are enlightening because they show how the presence of police stations does not affect the distribution of crimes, specifically sex assaults and homicides across the city of Chicago. There are also enlightening because the show the high number of sexual assaults and homicides registered in the first 5 months of 2018, which is striking, and that while the homicides are concentrated in more dangerous and less wealthy areas of the city like the south and the west side, sexual assaults are evenly distributed across the city.
