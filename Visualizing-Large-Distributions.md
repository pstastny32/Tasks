---
title: "Visualizing Large Distributions"
author: "Payton Stastny"
date: "April 25, 2022"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---






```r
# Use this R-Chunk to import all your datasets!
nycflights13::flights
```

```
## # A tibble: 336,776 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      517            515         2      830            819
##  2  2013     1     1      533            529         4      850            830
##  3  2013     1     1      542            540         2      923            850
##  4  2013     1     1      544            545        -1     1004           1022
##  5  2013     1     1      554            600        -6      812            837
##  6  2013     1     1      554            558        -4      740            728
##  7  2013     1     1      555            600        -5      913            854
##  8  2013     1     1      557            600        -3      709            723
##  9  2013     1     1      557            600        -3      838            846
## 10  2013     1     1      558            600        -2      753            745
## # … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>
```
## Univariate 1

The first univariate display i wanted to look at was the number of flights each carrier has.

```r
# Use this R-Chunk to clean & wrangle your data!
ggplot(data = nycflights13::flights) +
  geom_bar(mapping = aes(x = fct_infreq(carrier)))
```

![](Visualizing-Large-Distributions_files/figure-html/plot_data.1-1.png)<!-- -->

## Univariate 2

The second univariate display i wanted to look at was the amount of delayed departures


```r
# Use this R-Chunk to plot & visualize your data!

ggplot(data = nycflights13::flights,
      aes(x = dep_delay)) +
  geom_histogram(
    color = "white",
    binwidth = 10) +
  coord_cartesian(
    xlim = c(-25, 250))
```

![](Visualizing-Large-Distributions_files/figure-html/plot_data.2-1.png)<!-- -->

## Bivariate Graph

This zoomed in box plot graph shows us the quartiles in which carriers have late departures or on time departures.


```r
# Use this R-Chunk for bivariate plot
ggplot(data = nycflights13::flights) +
  aes(x = fct_reorder(carrier, dep_delay, na.rm = TRUE)) +
  aes(y = dep_delay) +
 geom_boxplot() +
  coord_cartesian(ylim = c(-50,250))
```

![](Visualizing-Large-Distributions_files/figure-html/plot_data.3-1.png)<!-- -->

## Conclusions

From the data that i picked out and summerized into these graphs, i have been able to find out identify what carriers have more departure delays than others and using the boxplot, i can know what percentage of carriers flights have delays or are ahead of schedule on average. Like we can see that 75% of HA and US have flights ahead of schedule.
