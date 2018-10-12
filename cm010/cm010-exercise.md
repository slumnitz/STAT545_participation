cm010 Exercises
================

## Install `nycflights13` package

``` r
install.packages("nycflights13")
```

``` r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(nycflights13))
```

## Types of mutating join

### Let’s join tibbles using four mutating functions: `left_join`, `right_join`, `inner_join` and `full_join`.

### create two tibbles named `a` and `b`

``` r
(a <- tibble(x1 = LETTERS[1:3], x2 = 1:3))
```

    ## # A tibble: 3 x 2
    ##   x1       x2
    ##   <chr> <int>
    ## 1 A         1
    ## 2 B         2
    ## 3 C         3

``` r
(b <- tibble(x1 = LETTERS[c(1,2,4)], x3 = c("T", "F", "T")))
```

    ## # A tibble: 3 x 2
    ##   x1    x3   
    ##   <chr> <chr>
    ## 1 A     T    
    ## 2 B     F    
    ## 3 D     T

### left\_join: Join matching rows from `b` to `a` by matching “x1” variable

### right\_join: Join matching rows from `a` to `b` by matching “x1” variable.

### inner\_join: Join data. Retain only rows in both sets `a` to `b` by matching “x1” variable.

### full\_join: Join data. Retain all values, all rows of `a` to `b` by matching “x1”

### what happen if we do not specify `by` option?

### what happen if we join two different variables (e.g., “x1” to “x3”) from two tibbles `a` to `b`?

### what happen if two columns of `a` and `c` datasets have the identical colnames?

``` r
# make data frame c and use inner_join()
(c <- tibble(x1 = c(LETTERS[1:2],"x"), x2 = c(1,4,5)))
```

    ## # A tibble: 3 x 2
    ##   x1       x2
    ##   <chr> <dbl>
    ## 1 A         1
    ## 2 B         4
    ## 3 x         5

## In class practice

`nycflights13` dataset has several tibbles e.g., `flights`, `airports`,
`planes`, `weather`.

### 1\. Explore `nycflights13` dataset

``` r
#check the tibbles included in `nycflights13` package
class(flights)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

``` r
colnames(flights)
```

    ##  [1] "year"           "month"          "day"            "dep_time"      
    ##  [5] "sched_dep_time" "dep_delay"      "arr_time"       "sched_arr_time"
    ##  [9] "arr_delay"      "carrier"        "flight"         "tailnum"       
    ## [13] "origin"         "dest"           "air_time"       "distance"      
    ## [17] "hour"           "minute"         "time_hour"

``` r
colnames(airlines)
```

    ## [1] "carrier" "name"

``` r
colnames(weather)
```

    ##  [1] "origin"     "year"       "month"      "day"        "hour"      
    ##  [6] "temp"       "dewp"       "humid"      "wind_dir"   "wind_speed"
    ## [11] "wind_gust"  "precip"     "pressure"   "visib"      "time_hour"

### 2\. Drop unimportant variables so it’s easier to understand the join results. Also take first 1000 rows to run it faster.

``` r
flights2 <- flights[1:1000,] %>% 
  select(year, tailnum, carrier, time_hour)
```

### 3\. Add airline names to `flights2` from `airlines` dataset.

``` r
# Which join function to use?
```

### 4\. Add `weather` information to the `flights2` dataset by matching “year” and “time\_hour” variables.

### 5\. Add `weather` information to the `flights2` dataset by matching only “time\_hour” variable

## Types of filtering join

### Let’s filter tibbles using two filtering functions: `semi_join`, `anti_join`

### example for `semi_join`: All rows in `a` that have a match in `b`

### example for `anti_join`: All rows in `a` that do not have a match in `b`

### example of joinin by matching two variables (e.g., “x1”, “x2”) from both datasets `a` and `c`

## Types of Set Operations for two datasets

### Let’s use three `set` functions: `intersect`, `union` and `setdiff`

### create two tibbles named `y` and `z`, similar to Data Wrangling Cheatsheet

``` r
(y <-  tibble(x1 = LETTERS[1:3], x2 = 1:3))
```

    ## # A tibble: 3 x 2
    ##   x1       x2
    ##   <chr> <int>
    ## 1 A         1
    ## 2 B         2
    ## 3 C         3

``` r
(z <- tibble(x1 = c("B", "C", "D"), x2 = 2:4))
```

    ## # A tibble: 3 x 2
    ##   x1       x2
    ##   <chr> <int>
    ## 1 B         2
    ## 2 C         3
    ## 3 D         4

### example for `intersect`: Rows that appear in both `y` and `z`

### example for `union`: Rows that appear in either or both `y` and `z`

### example for `setdiff`: Rows that appear in `y` but not `z`. **Caution:** `setdiff` for `y` to `z` and `z` to `y` are different.

### what happen if colnames are differentin `y` and `x`? Is there any error message and why?

``` r
(x <- tibble(x1 = c("B", "C", "D"), x3 = 2:4))
```

    ## # A tibble: 3 x 2
    ##   x1       x3
    ##   <chr> <int>
    ## 1 B         2
    ## 2 C         3
    ## 3 D         4

## Types of binding datasets

### Let’s bind datasets by rows or column using two binding functions:

### example for `bind_rows`: Append `z` to `y` as new rows

### example for `bind_cols`: Append `z` to `y` as new columns. **Caution**: matches rows by position. Check colnames after binding.

### what happen if colnames are different between `y` and `x` datasets?

\#\#Practice Exercises Practice these concepts in the following
exercises. It might help you to first identify the type of function you
are
applying.

### 1\. Filter the rows of `flights2` by matching “year” and “time\_hour” variables to `weather` dataset. Use both `semi_join()` and `anti_join()`

### 2\. Can we apply `set` and `binding` funcions between `flights2` and `weather` datasets. Why and why not?

### 3\. Let’s create a tibble `p` with “x1” and “x2” coulmns and have duplicated element in “x1” column. Create another tibble `q` with “x1” and “x3” columns. Then apply `left_join` function `p` to `q` and `q` to `p`.
