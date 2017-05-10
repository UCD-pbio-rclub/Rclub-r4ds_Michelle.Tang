---
title: "R4ds_May10"
author: "Michelle Tang"
date: "5/9/2017"
output: html_document
---

##Data transformation




```r
flights
```

```
## # A tibble: 336,776 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1      517            515         2      830
## 2   2013     1     1      533            529         4      850
## 3   2013     1     1      542            540         2      923
## 4   2013     1     1      544            545        -1     1004
## 5   2013     1     1      554            600        -6      812
## 6   2013     1     1      554            558        -4      740
## 7   2013     1     1      555            600        -5      913
## 8   2013     1     1      557            600        -3      709
## 9   2013     1     1      557            600        -3      838
## 10  2013     1     1      558            600        -2      753
## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

**Five Key Functions**

*Pick observations by their values (filter()).
*Reorder the rows (arrange()).
*Pick variables by their names (select()).
*Create new variables with functions of existing variables (mutate()).
*Collapse many values down to a single summary (summarise()).


```r
filter(flights, month==1, sched_dep_time==515)
```

```
## # A tibble: 6 × 19
##    year month   day dep_time sched_dep_time dep_delay arr_time
##   <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1  2013     1     1      517            515         2      830
## 2  2013     1     2      512            515        -3      809
## 3  2013     1     5      516            515         1      821
## 4  2013     1    12      521            515         6      755
## 5  2013     1    19      623            515        68      902
## 6  2013     1    26      520            515         5      756
## # ... with 12 more variables: sched_arr_time <int>, arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>,
## #   time_hour <dttm>
```

For other types of combinations, you’ll need to use Boolean operators yourself: & is “and”, | is “or”, and ! is “not”.

== versus near()
near() is an approximation

###5.2.4 Exercises

1. Find all flights that

  + Had an arrival delay of two or more hours
  

```r
filter(flights, arr_delay >=120)
```

```
## # A tibble: 10,200 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1      811            630       101     1047
## 2   2013     1     1      848           1835       853     1001
## 3   2013     1     1      957            733       144     1056
## 4   2013     1     1     1114            900       134     1447
## 5   2013     1     1     1505           1310       115     1638
## 6   2013     1     1     1525           1340       105     1831
## 7   2013     1     1     1549           1445        64     1912
## 8   2013     1     1     1558           1359       119     1718
## 9   2013     1     1     1732           1630        62     2028
## 10  2013     1     1     1803           1620       103     2008
## # ... with 10,190 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

  + Flew to Houston (IAH or HOU)
  

```r
filter(flights, dest=="IAH" | dest=="HOU")
```

```
## # A tibble: 9,313 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1      517            515         2      830
## 2   2013     1     1      533            529         4      850
## 3   2013     1     1      623            627        -4      933
## 4   2013     1     1      728            732        -4     1041
## 5   2013     1     1      739            739         0     1104
## 6   2013     1     1      908            908         0     1228
## 7   2013     1     1     1028           1026         2     1350
## 8   2013     1     1     1044           1045        -1     1352
## 9   2013     1     1     1114            900       134     1447
## 10  2013     1     1     1205           1200         5     1503
## # ... with 9,303 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

  + Were operated by United, American, or Delta


```r
filter(flights, carrier == "UA" | carrier == "AA" | carrier =="DL")
```

```
## # A tibble: 139,504 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1      517            515         2      830
## 2   2013     1     1      533            529         4      850
## 3   2013     1     1      542            540         2      923
## 4   2013     1     1      554            600        -6      812
## 5   2013     1     1      554            558        -4      740
## 6   2013     1     1      558            600        -2      753
## 7   2013     1     1      558            600        -2      924
## 8   2013     1     1      558            600        -2      923
## 9   2013     1     1      559            600        -1      941
## 10  2013     1     1      559            600        -1      854
## # ... with 139,494 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

  + Departed in summer (July, August, and September)
  

```r
filter(flights, month %in% c(7,8,9))
```

```
## # A tibble: 86,326 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     7     1        1           2029       212      236
## 2   2013     7     1        2           2359         3      344
## 3   2013     7     1       29           2245       104      151
## 4   2013     7     1       43           2130       193      322
## 5   2013     7     1       44           2150       174      300
## 6   2013     7     1       46           2051       235      304
## 7   2013     7     1       48           2001       287      308
## 8   2013     7     1       58           2155       183      335
## 9   2013     7     1      100           2146       194      327
## 10  2013     7     1      100           2245       135      337
## # ... with 86,316 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

  + Arrived more than two hours late, but didn’t leave late
  

```r
filter(flights, arr_delay >= 120 & dep_delay <= 0)
```

```
## # A tibble: 29 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1    27     1419           1420        -1     1754
## 2   2013    10     7     1350           1350         0     1736
## 3   2013    10     7     1357           1359        -2     1858
## 4   2013    10    16      657            700        -3     1258
## 5   2013    11     1      658            700        -2     1329
## 6   2013     3    18     1844           1847        -3       39
## 7   2013     4    17     1635           1640        -5     2049
## 8   2013     4    18      558            600        -2     1149
## 9   2013     4    18      655            700        -5     1213
## 10  2013     5    22     1827           1830        -3     2217
## # ... with 19 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

  + Were delayed by at least an hour, but made up over 30 minutes in flight (not sure what the second half means)
  

```r
filter(flights, dep_delay >= 60 & sched_arr_time-arr_time > 30)
```

```
## # A tibble: 4,608 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1      848           1835       853     1001
## 2   2013     1     1     2205           1720       285       46
## 3   2013     1     1     2312           2000       192       21
## 4   2013     1     1     2323           2200        83       22
## 5   2013     1     1     2343           1724       379      314
## 6   2013     1     2      126           2250       156      233
## 7   2013     1     2     2145           1925       140       54
## 8   2013     1     2     2225           1930       175      231
## 9   2013     1     2     2259           2100       119      122
## 10  2013     1     2     2309           2200        69        5
## # ... with 4,598 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

  
  + Departed between midnight and 6am (inclusive)
  

```r
filter(flights, dep_time >= 0 & dep_time <= 600)
```

```
## # A tibble: 9,344 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1      517            515         2      830
## 2   2013     1     1      533            529         4      850
## 3   2013     1     1      542            540         2      923
## 4   2013     1     1      544            545        -1     1004
## 5   2013     1     1      554            600        -6      812
## 6   2013     1     1      554            558        -4      740
## 7   2013     1     1      555            600        -5      913
## 8   2013     1     1      557            600        -3      709
## 9   2013     1     1      557            600        -3      838
## 10  2013     1     1      558            600        -2      753
## # ... with 9,334 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```


2. Another useful dplyr filtering helper is between(). What does it do? Can you use it to simplify the code needed to answer the previous challenges?

includes values inside upper and lower boundaries.


```r
?between
filter(flights, between(dep_time, 0, 600))
```

```
## # A tibble: 9,344 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1      517            515         2      830
## 2   2013     1     1      533            529         4      850
## 3   2013     1     1      542            540         2      923
## 4   2013     1     1      544            545        -1     1004
## 5   2013     1     1      554            600        -6      812
## 6   2013     1     1      554            558        -4      740
## 7   2013     1     1      555            600        -5      913
## 8   2013     1     1      557            600        -3      709
## 9   2013     1     1      557            600        -3      838
## 10  2013     1     1      558            600        -2      753
## # ... with 9,334 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

3. How many flights have a missing dep_time? What other variables are missing? What might these rows represent?


```r
filter(flights, is.na(dep_time))
```

```
## # A tibble: 8,255 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1       NA           1630        NA       NA
## 2   2013     1     1       NA           1935        NA       NA
## 3   2013     1     1       NA           1500        NA       NA
## 4   2013     1     1       NA            600        NA       NA
## 5   2013     1     2       NA           1540        NA       NA
## 6   2013     1     2       NA           1620        NA       NA
## 7   2013     1     2       NA           1355        NA       NA
## 8   2013     1     2       NA           1420        NA       NA
## 9   2013     1     2       NA           1321        NA       NA
## 10  2013     1     2       NA           1545        NA       NA
## # ... with 8,245 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

Other variables that are missing data is dep_delay, arr_time, arr_delay, air_time
These might be canceled flights

4. Why is NA ^ 0 not missing? Why is NA | TRUE not missing? Why is FALSE & NA not missing? Can you figure out the general rule? (NA * 0 is a tricky counterexample!)

Because anything to the 0 power is 1
Because NA | TRUE includes TRUE which is not missing
FALSE, like NA is a logical object. 
Input of logical object and NA with logical operators will return another logical object
NA * 0 might not work because NA could be anything, not just a number and not a logical object

###5.3.1 Exercises

1. How could you use arrange() to sort all missing values to the start? (Hint: use is.na()).


```r
arrange(flights, desc(is.na(dep_time)))
```

```
## # A tibble: 336,776 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1       NA           1630        NA       NA
## 2   2013     1     1       NA           1935        NA       NA
## 3   2013     1     1       NA           1500        NA       NA
## 4   2013     1     1       NA            600        NA       NA
## 5   2013     1     2       NA           1540        NA       NA
## 6   2013     1     2       NA           1620        NA       NA
## 7   2013     1     2       NA           1355        NA       NA
## 8   2013     1     2       NA           1420        NA       NA
## 9   2013     1     2       NA           1321        NA       NA
## 10  2013     1     2       NA           1545        NA       NA
## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```


2. Sort flights to find the most delayed flights. Find the flights that left earliest.


```r
arrange(flights, desc(dep_delay), dep_time)
```

```
## # A tibble: 336,776 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     9      641            900      1301     1242
## 2   2013     6    15     1432           1935      1137     1607
## 3   2013     1    10     1121           1635      1126     1239
## 4   2013     9    20     1139           1845      1014     1457
## 5   2013     7    22      845           1600      1005     1044
## 6   2013     4    10     1100           1900       960     1342
## 7   2013     3    17     2321            810       911      135
## 8   2013     6    27      959           1900       899     1236
## 9   2013     7    22     2257            759       898      121
## 10  2013    12     5      756           1700       896     1058
## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

3. Sort flights to find the fastest flights.


```r
arrange(flights, air_time)
```

```
## # A tibble: 336,776 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1    16     1355           1315        40     1442
## 2   2013     4    13      537            527        10      622
## 3   2013    12     6      922            851        31     1021
## 4   2013     2     3     2153           2129        24     2247
## 5   2013     2     5     1303           1315       -12     1342
## 6   2013     2    12     2123           2130        -7     2211
## 7   2013     3     2     1450           1500       -10     1547
## 8   2013     3     8     2026           1935        51     2131
## 9   2013     3    18     1456           1329        87     1533
## 10  2013     3    19     2226           2145        41     2305
## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

4. Which flights travelled the longest? Which travelled the shortest?


```r
arrange(flights, desc(distance))
```

```
## # A tibble: 336,776 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1      857            900        -3     1516
## 2   2013     1     2      909            900         9     1525
## 3   2013     1     3      914            900        14     1504
## 4   2013     1     4      900            900         0     1516
## 5   2013     1     5      858            900        -2     1519
## 6   2013     1     6     1019            900        79     1558
## 7   2013     1     7     1042            900       102     1620
## 8   2013     1     8      901            900         1     1504
## 9   2013     1     9      641            900      1301     1242
## 10  2013     1    10      859            900        -1     1449
## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

```r
arrange(flights, distance)
```

```
## # A tibble: 336,776 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     7    27       NA            106        NA       NA
## 2   2013     1     3     2127           2129        -2     2222
## 3   2013     1     4     1240           1200        40     1333
## 4   2013     1     4     1829           1615       134     1937
## 5   2013     1     4     2128           2129        -1     2218
## 6   2013     1     5     1155           1200        -5     1241
## 7   2013     1     6     2125           2129        -4     2224
## 8   2013     1     7     2124           2129        -5     2212
## 9   2013     1     8     2127           2130        -3     2304
## 10  2013     1     9     2126           2129        -3     2217
## # ... with 336,766 more rows, and 12 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>
```

###5.4.1 Exercises

1. Brainstorm as many ways as possible to select dep_time, dep_delay, arr_time, and arr_delay from flights.


```r
select(flights, dep_time, dep_delay, arr_time, arr_delay)
```

```
## # A tibble: 336,776 × 4
##    dep_time dep_delay arr_time arr_delay
##       <int>     <dbl>    <int>     <dbl>
## 1       517         2      830        11
## 2       533         4      850        20
## 3       542         2      923        33
## 4       544        -1     1004       -18
## 5       554        -6      812       -25
## 6       554        -4      740        12
## 7       555        -5      913        19
## 8       557        -3      709       -14
## 9       557        -3      838        -8
## 10      558        -2      753         8
## # ... with 336,766 more rows
```

```r
select(flights, dep_time, dep_delay:arr_time, arr_delay)
```

```
## # A tibble: 336,776 × 4
##    dep_time dep_delay arr_time arr_delay
##       <int>     <dbl>    <int>     <dbl>
## 1       517         2      830        11
## 2       533         4      850        20
## 3       542         2      923        33
## 4       544        -1     1004       -18
## 5       554        -6      812       -25
## 6       554        -4      740        12
## 7       555        -5      913        19
## 8       557        -3      709       -14
## 9       557        -3      838        -8
## 10      558        -2      753         8
## # ... with 336,766 more rows
```

```r
select(flights, -(year:day), -(sched_dep_time),-(sched_arr_time), -(carrier:time_hour))
```

```
## # A tibble: 336,776 × 4
##    dep_time dep_delay arr_time arr_delay
##       <int>     <dbl>    <int>     <dbl>
## 1       517         2      830        11
## 2       533         4      850        20
## 3       542         2      923        33
## 4       544        -1     1004       -18
## 5       554        -6      812       -25
## 6       554        -4      740        12
## 7       555        -5      913        19
## 8       557        -3      709       -14
## 9       557        -3      838        -8
## 10      558        -2      753         8
## # ... with 336,766 more rows
```

2. What happens if you include the name of a variable multiple times in a select() call?


```r
select(flights, day, day, day)
```

```
## # A tibble: 336,776 × 1
##      day
##    <int>
## 1      1
## 2      1
## 3      1
## 4      1
## 5      1
## 6      1
## 7      1
## 8      1
## 9      1
## 10     1
## # ... with 336,766 more rows
```

```r
select(flights, carrier, day, carrier)
```

```
## # A tibble: 336,776 × 2
##    carrier   day
##      <chr> <int>
## 1       UA     1
## 2       UA     1
## 3       AA     1
## 4       B6     1
## 5       DL     1
## 6       UA     1
## 7       B6     1
## 8       EV     1
## 9       B6     1
## 10      AA     1
## # ... with 336,766 more rows
```

It gets selected only once.

3. What does the one_of() function do? Why might it be helpful in conjunction with this vector?


```r
?one_of
```

Allows selecting variables contained in a character vector.


```r
vars <- c("year", "month", "day", "dep_delay", "arr_delay")

select(flights, one_of(vars))
```

```
## # A tibble: 336,776 × 5
##     year month   day dep_delay arr_delay
##    <int> <int> <int>     <dbl>     <dbl>
## 1   2013     1     1         2        11
## 2   2013     1     1         4        20
## 3   2013     1     1         2        33
## 4   2013     1     1        -1       -18
## 5   2013     1     1        -6       -25
## 6   2013     1     1        -4        12
## 7   2013     1     1        -5        19
## 8   2013     1     1        -3       -14
## 9   2013     1     1        -3        -8
## 10  2013     1     1        -2         8
## # ... with 336,766 more rows
```


4. Does the result of running the following code surprise you? How do the select helpers deal with case by default? How can you change that default?


```r
select(flights, contains("TIME"))
```

```
## # A tibble: 336,776 × 6
##    dep_time sched_dep_time arr_time sched_arr_time air_time
##       <int>          <int>    <int>          <int>    <dbl>
## 1       517            515      830            819      227
## 2       533            529      850            830      227
## 3       542            540      923            850      160
## 4       544            545     1004           1022      183
## 5       554            600      812            837      116
## 6       554            558      740            728      150
## 7       555            600      913            854      158
## 8       557            600      709            723       53
## 9       557            600      838            846      140
## 10      558            600      753            745      138
## # ... with 336,766 more rows, and 1 more variables: time_hour <dttm>
```

By default, contains() ignores case in argument ignore.case = TRUE. Can change to FALSE if need to match case.

###5.5.2 Exercises

1. Currently dep_time and sched_dep_time are convenient to look at, but hard to compute with because they’re not really continuous numbers. Convert them to a more convenient representation of number of minutes since midnight.


```r
transmute(flights, dep_time, dep_midnight = dep_time %/% 100 * 60 + dep_time %% 100)
```

```
## # A tibble: 336,776 × 2
##    dep_time dep_midnight
##       <int>        <dbl>
## 1       517          317
## 2       533          333
## 3       542          342
## 4       544          344
## 5       554          354
## 6       554          354
## 7       555          355
## 8       557          357
## 9       557          357
## 10      558          358
## # ... with 336,766 more rows
```

```r
transmute(flights, sched_dep_time, sched_dep_midnight = sched_dep_time %/% 100 * 60 + sched_dep_time %% 100)
```

```
## # A tibble: 336,776 × 2
##    sched_dep_time sched_dep_midnight
##             <int>              <dbl>
## 1             515                315
## 2             529                329
## 3             540                340
## 4             545                345
## 5             600                360
## 6             558                358
## 7             600                360
## 8             600                360
## 9             600                360
## 10            600                360
## # ... with 336,766 more rows
```


2. Compare air_time with arr_time - dep_time. What do you expect to see? What do you see? What do you need to do to fix it?


```r
select(flights, air_time) 
```

```
## # A tibble: 336,776 × 1
##    air_time
##       <dbl>
## 1       227
## 2       227
## 3       160
## 4       183
## 5       116
## 6       150
## 7       158
## 8        53
## 9       140
## 10      138
## # ... with 336,766 more rows
```

```r
mutate(flights, arr_time - dep_time)
```

```
## # A tibble: 336,776 × 20
##     year month   day dep_time sched_dep_time dep_delay arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>
## 1   2013     1     1      517            515         2      830
## 2   2013     1     1      533            529         4      850
## 3   2013     1     1      542            540         2      923
## 4   2013     1     1      544            545        -1     1004
## 5   2013     1     1      554            600        -6      812
## 6   2013     1     1      554            558        -4      740
## 7   2013     1     1      555            600        -5      913
## 8   2013     1     1      557            600        -3      709
## 9   2013     1     1      557            600        -3      838
## 10  2013     1     1      558            600        -2      753
## # ... with 336,766 more rows, and 13 more variables: sched_arr_time <int>,
## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>,
## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
## #   minute <dbl>, time_hour <dttm>, `arr_time - dep_time` <int>
```

They don't equal to each other.
To fix it, need to change arr_time and dep_time to minutes after minute and then substract.


3. Compare dep_time, sched_dep_time, and dep_delay. How would you expect those three numbers to be related?


```r
select(flights, dep_time, sched_dep_time, dep_delay)
```

```
## # A tibble: 336,776 × 3
##    dep_time sched_dep_time dep_delay
##       <int>          <int>     <dbl>
## 1       517            515         2
## 2       533            529         4
## 3       542            540         2
## 4       544            545        -1
## 5       554            600        -6
## 6       554            558        -4
## 7       555            600        -5
## 8       557            600        -3
## 9       557            600        -3
## 10      558            600        -2
## # ... with 336,766 more rows
```

delay_delay = dep_time - sched_dep_time

4. Find the 10 most delayed flights using a ranking function. How do you want to handle ties? Carefully read the documentation for min_rank().


```
##    [1] 114150 103893 114150 144947 258934 209494 234113 185276 185276
##   [10] 163760 163760 163760 163760 163760 144947 128433 144947 128433
##   [19] 128433 120383 296387 185276 209494 209494 128433  88756  80079
##   [28] 108700 128433 128433 296387  75171 209494 258934 258934 185276
##   [37] 163760 163760 144947 144947 144947  55691 128433 296387 144947
##   [46] 185276 163760  88756 163760 120383 120383 209494 185276 279635
##   [55] 128433 234113 234113 209494 185276 308178 209494 185276 163760
##   [64] 163760 144947 144947 258934 144947 120383 114150  85694 209494
##   [73] 185276 114150 185276 163760 163760 258934 144947 234113 185276
##   [82] 209494 144947 185276 108700  33948 185276 185276 258934 128433
##   [91] 209494  75171 258934  75171 128433 128433  39842 185276 114150
##  [100] 279635 163760 234113 144947 163760 144947 128433 316053 209494
##  [109] 279635 108700 258934 128433  99446 316053 185276 258934 128433
##  [118] 234113 209494  13141 209494 163760 163760 103893  92137 128433
##  [127] 316053 128433 120383 209494 296387 163760 128433 258934 163760
##  [136]  21796  85694 163760  99446 144947 144947 128433 234113 209494
##  [145] 296387 163760 128433 321944 234113 234113 120383     12 185276
##  [154] 128433 296387  80079 185276  88756 209494 209494 209494 120383
##  [163] 185276 296387 185276  95657 163760 144947 144947 128433 144947
##  [172]  36725 163760 128433  57135 163760 279635 128433  27060  77585
##  [181]  95657 234113 258934  72915 185276 114150 185276  70775 128433
##  [190]  60037 103893 185276 103893 163760 185276 128433 103893  54348
##  [199] 120383 120383 114150 209494  49414 163760 209494 308178 185276
##  [208] 185276 234113 327664 209494 326265 258934 209494 258934  46175
##  [217] 234113 209494   6727 185276 144947 279635 103893  99446 185276
##  [226] 258934 234113 234113  82835 209494 163760 234113 258934  99446
##  [235]  44162 209494 114150 144947 234113 120383 120383 185276  68690
##  [244]  92137  88756 114150 144947 144947 108700 296387 185276 163760
##  [253] 108700 234113 185276 209494 163760 144947 144947  95657  65068
##  [262] 108700  65068 296387 258934 209494  77585 163760   7804  14286
##  [271] 234113  75171  55691 144947 234113 163760 185276 163760 144947
##  [280]  99446 144947 185276 103893 108700 234113 185276 163760 144947
##  [289] 296387 258934 258934  48292 279635 258934 258934 234113 234113
##  [298] 234113 234113 144947 296387 185276 279635 163760 163760 128433
##  [307] 234113 108700 163760 108700 103893  99446 185276  82835 209494
##  [316] 185276 144947 144947 258934 128433  57135 279635 103893 234113
##  [325] 279635 114150 296387 163760  80079 234113  99446 258934 128433
##  [334] 209494  60037 163760 144947  92137  38264 234113 128433  29224
##  [343] 209494 234113 144947 185276 316053 163760  60037  21796  95657
##  [352] 108700 114150  41528  99446 316053  53049  95657  82835 144947
##  [361] 163760 114150 296387 209494  99446 128433  57135 234113 185276
##  [370] 163760  85694 163760 209494  19691 258934 103893 209494  58540
##  [379]  75171 128433  68690  60037 234113 209494 209494 163760 234113
##  [388]  39032 144947  99446  95657  28119 114150  95657  88756  22174
##  [397] 128433  39842 185276  28663  99446 144947 144947 144947  53049
##  [406] 308178  77585 185276 279635  43213 103893  27060  47184 128433
##  [415] 114150 308178 163760 120383 258934 128433 296387 144947 316053
##  [424] 128433 308178 108700 144947 308178 185276 234113 108700 279635
##  [433] 209494 258934 258934 163760 209494 234113 209494 120383 185276
##  [442] 185276 163760 163760  99446 120383 114150  10509 234113 120383
##  [451] 258934 296387 185276  65068 279635  80079 209494 258934  88756
##  [460] 163760  40677 114150  32074 234113 128433  95657 296387 296387
##  [469]  92137  51776  12326 234113 209494 185276  46175 258934  77585
##  [478]  49414 163760  46175 144947 128433  40677  46175  80079 103893
##  [487]  68690 163760  85694 258934 114150   9404 185276 279635 128433
##  [496]  95657 114150  16332  24706 120383 128433 296387 296387 296387
##  [505] 296387 258934 234113 258934 209494 185276 185276  55691   9889
##  [514] 163760 258934 316053 128433 185276  68690  75171 108700 163760
##  [523] 108700  29765 234113  77585  17480  45136  88756 144947 234113
##  [532] 234113  70775  82835  75171 258934 128433  45136 108700  43213
##  [541] 209494 209494  16332 185276  24706 163760  37501 258934  72915
##  [550] 209494 120383 185276 185276  88756  99446 185276  30889  18070
##  [559] 128433 308178  46175  95657  82835  43213 120383  77585 279635
##  [568]  82835 258934  44162 234113 234113 128433 209494  92137  51776
##  [577] 163760 308178 120383 114150 128433 234113 114150  92137  88756
##  [586]  60037  42356  21796 279635  77585  75171 258934 327166  15523
##  [595]  92137 185276  88756 144947 234113 234113  99446 209494 185276
##  [604] 114150  16332  80079 128433 128433 120383  25632  28663 279635
##  [613] 258934 144947  22174 234113 209494  16332 258934  55691 144947
##  [622] 144947 209494 128433  95657  95657  88756  47184  29765 163760
##  [631] 163760 163760  85694 128433 128433 128433 185276 120383  41528
##  [640]  12742 108700  88756 209494  49414 279635 144947  77585  20708
##  [649] 144947    712  82835  80079  68690 185276 128433 279635 258934
##  [658] 209494 209494  68690 209494 163760  57135 120383  85694 185276
##  [667] 103893 258934  44162  22174 103893 234113 234113   1132  75171
##  [676] 279635 163760  88756  26100 308178  25164 321944 316053 128433
##  [685] 128433 279635  55691 209494  92137   8184 185276 120383 163760
##  [694] 144947 144947  70775 144947 144947  99446 308178 185276 144947
##  [703] 120383 128433  70775 120383 185276 103893 234113  80079 209494
##  [712]  63338 120383  34607  55691 234113  54348  68690 163760  85694
##  [721]  12326   8416  99446  46175   5732  27060 144947  43213 120383
##  [730]   5564  99446  68690  32074  58540 296387  58540 234113 296387
##  [739]  77585 185276  49414 144947  48292 128433  92137 108700   2211
##  [748]  95657  21061 279635   9557 209494 163760  82835  34607  42356
##  [757]  37501 114150 163760 316053 209494  40677  11599 234113 185276
##  [766]  58540  28663  47184 128433 327664 234113 128433 120383 144947
##  [775]  99446  51776 128433  80079 209494  31438  57135  92137 163760
##  [784] 234113  30889  21432 209494 209494 185276 163760 163760 163760
##  [793] 128433  80079 258934 279635  51776  80079 258934  32074  99446
##  [802]   1221  95657  11599 316053  38264 185276 279635 108700  85694
##  [811]  32730 308178  99446 114150 163760    773  55691  72915  53049
##  [820] 324671  33948   7028  55691  48292 234113 234113  25632  60037
##  [829]  58540  70775   3215  17780  10355  41528    189 258934 258934
##  [838] 185276     NA     NA     NA     NA  36725   5642 163760 185276
##  [847] 234113  92137 258934 258934 258934 258934 234113 234113 234113
##  [856] 209494 209494 296387 163760 163760 163760 144947 128433 234113
##  [865] 128433 128433 128433 234113 128433 114150 108700 103893  99446
##  [874] 209494 209494 185276  85694  82835 234113  80079  77585 185276
##  [883]  68690 114150  80079 296387  55691 234113 209494 234113 209494
##  [892] 163760  75171  72915  85694 144947  61634 234113 128433 185276
##  [901] 114150 103893 144947  99446 185276  92137  95657 128433 258934
##  [910]  95657  95657 258934 209494  77585 114150 120383 114150 258934
##  [919] 163760 258934 108700 209494 128433 234113 234113 234113 209494
##  [928] 308178 185276 144947  48292 128433 128433 209494 114150  85694
##  [937] 144947 103893  43213 234113 296387  85694  77585  77585 144947
##  [946] 258934 128433 144947  18700 185276  82835 258934  37501 163760
##  [955]  85694 128433 144947  70775 114150 209494 128433 163760 209494
##  [964]  44162 114150 296387 279635 258934 103893 128433 163760 120383
##  [973] 163760  72915  70775 144947 163760  54348 308178 296387 296387
##  [982]  92137  19044 144947 234113 234113 209494 185276 163760 108700
##  [991] 258934 316053  47184 308178 144947 209494 185276 163760 279635
## [1000] 144947
##  [ reached getOption("max.print") -- omitted 335776 entries ]
```

To handle ties, can use variation of min_rank(). min_rank has gaps in ranks for ties. Can use row_number or dense_rank

5. What does 1:3 + 1:10 return? Why?


```r
#1:3 + 1:10
```

It cycles 1 through 3 and adds to 1 through 10 but it gives error because 10 isn't a mulitple of 3

6. What trigonometric functions does R provide?

```
cos(x)
sin(x)
tan(x)

acos(x)
asin(x)
atan(x)
atan2(y, x)

cospi(x)
sinpi(x)
tanpi(x)
```
