---
title: "R_Club_DataVis"
author: "Michelle Tang"
date: "4/24/2017"
output: html_document
---
Exercises from 'R for Data Science', Data Visualization to end of 3.5.1.

3.1.1

Load tidyverse, install package if needed.



3.2.1
Do cars with big engines use more fuel than cars with small engines?


```r
mpg<-mpg
head(mpg)
```

```
## # A tibble: 6 × 11
##   manufacturer model displ  year   cyl      trans   drv   cty   hwy    fl
##          <chr> <chr> <dbl> <int> <int>      <chr> <chr> <int> <int> <chr>
## 1         audi    a4   1.8  1999     4   auto(l5)     f    18    29     p
## 2         audi    a4   1.8  1999     4 manual(m5)     f    21    29     p
## 3         audi    a4   2.0  2008     4 manual(m6)     f    20    31     p
## 4         audi    a4   2.0  2008     4   auto(av)     f    21    30     p
## 5         audi    a4   2.8  1999     6   auto(l5)     f    16    26     p
## 6         audi    a4   2.8  1999     6 manual(m5)     f    18    26     p
## # ... with 1 more variables: class <chr>
```

3.2.2 through 3.2.4

Scatterplot

```r
ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y = hwy))
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-1.png)

Graphing template
ggplot(data = <DATA>) + <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))

####3.2.4 Exercises

1. ggplot(data = mpg)


```r
ggplot(data = mpg)
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3-1.png)

An empty field

2. How many rows and columns in mtcar


```r
dim(mtcars)
```

```
## [1] 32 11
```

3. Describe drv variable


```r
?mpg
```

f = front wheel drive
r = rear wheel drive
4 = 4wd

4. Scatterplot of hwy vs cyl


```r
ggplot(data = mpg) + geom_point(mapping = aes(x = hwy, y = cyl))
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-1.png)

5. Scatterplot class vs drv


```r
ggplot(data = mpg) + geom_point(mapping = aes(x=class, y = drv))
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7-1.png)

Not useful as I don't see any trends or linear relationship.

3.3 Aesthetic mapping

```r
ggplot(data = mpg) + geom_point(mapping=aes(x=displ, y=hwy, color = class))
```

![plot of chunk unnamed-chunk-8](figure/unnamed-chunk-8-1.png)


```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, size = class))
```

```
## Warning: Using size for a discrete variable is not advised.
```

![plot of chunk unnamed-chunk-9](figure/unnamed-chunk-9-1.png)


```r
# Left
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, alpha = class))
```

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10-1.png)


```r
# Right
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, shape = class))
```

```
## Warning: The shape palette can deal with a maximum of 6 discrete values
## because more than 6 becomes difficult to discriminate; you have 7.
## Consider specifying shapes manually if you must have them.
```

```
## Warning: Removed 62 rows containing missing values (geom_point).
```

![plot of chunk unnamed-chunk-11](figure/unnamed-chunk-11-1.png)

####3.3.1 Exercises
1. What’s gone wrong with this code? Why are the points not blue?


```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))
```

![plot of chunk unnamed-chunk-12](figure/unnamed-chunk-12-1.png)

The color of points isn't blue. The color = "blue" is inside aes() so tried to map aesthics to a variable called "blue" which doesn't exist.

2. Which variables in mpg are categorical? Which continuous?

```r
str(mpg)
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	234 obs. of  11 variables:
##  $ manufacturer: chr  "audi" "audi" "audi" "audi" ...
##  $ model       : chr  "a4" "a4" "a4" "a4" ...
##  $ displ       : num  1.8 1.8 2 2 2.8 2.8 3.1 1.8 1.8 2 ...
##  $ year        : int  1999 1999 2008 2008 1999 1999 2008 1999 1999 2008 ...
##  $ cyl         : int  4 4 4 4 6 6 6 4 4 4 ...
##  $ trans       : chr  "auto(l5)" "manual(m5)" "manual(m6)" "auto(av)" ...
##  $ drv         : chr  "f" "f" "f" "f" ...
##  $ cty         : int  18 21 20 21 16 18 18 18 16 20 ...
##  $ hwy         : int  29 29 31 30 26 26 27 26 25 28 ...
##  $ fl          : chr  "p" "p" "p" "p" ...
##  $ class       : chr  "compact" "compact" "compact" "compact" ...
```


```r
?mpg
```

Categorical: manufacturer, model, class, fl, drv, trans, year, cyl
Continuous: cty, hwy, displ, year

3. Map a continuous variable to color, size and shape. How does these aesthetics behave?


```r
ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y = hwy, color = cty)) #continuous
```

![plot of chunk unnamed-chunk-15](figure/unnamed-chunk-15-1.png)


```r
ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y = hwy, color = drv)) #categorical
```

![plot of chunk unnamed-chunk-16](figure/unnamed-chunk-16-1.png)



```r
#ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y = hwy, shape = cty)) #continuous
```

```r
ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y = hwy, shape = drv)) #categorical
```

![plot of chunk unnamed-chunk-18](figure/unnamed-chunk-18-1.png)


```r
ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y = hwy, size = cty)) #continuous
```

![plot of chunk unnamed-chunk-19](figure/unnamed-chunk-19-1.png)


```r
ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y = hwy, size = drv)) 
```

```
## Warning: Using size for a discrete variable is not advised.
```

![plot of chunk unnamed-chunk-20](figure/unnamed-chunk-20-1.png)

Color: Gradient for continuous, discrete aesthetics for categorical. 
Size: Gradient for continous and categorical
Shape: Error for continuous and discrete for categorical

4. Map same variable to multiple aesthetics


```r
ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y = hwy, color = cty, size = cty)) 
```

![plot of chunk unnamed-chunk-21](figure/unnamed-chunk-21-1.png)

```r
ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y = hwy, color = drv, shape=drv)) 
```

![plot of chunk unnamed-chunk-22](figure/unnamed-chunk-22-1.png)

Possbile. For categorical, multiple aesthetics can be mapped and given one legend. FOr continous, excluding shape, get two legends.

5. What does stroke aesthetic do?

```r
?geom_point
```

To modify width of border for shapes that have a border.


```r
ggplot(mtcars, aes(wt, mpg)) +
  geom_point(shape = 21, colour = "black", fill = "white", size = 5, stroke = 5)
```

![plot of chunk unnamed-chunk-24](figure/unnamed-chunk-24-1.png)

```r
ggplot(mtcars, aes(wt, mpg)) +
  geom_point(shape = 21, colour = "black", fill = "white", size = 5)
```

![plot of chunk unnamed-chunk-25](figure/unnamed-chunk-25-1.png)

6. What happens if you map aesthic to somethign other than a variable?


```r
ggplot(data = mpg) +
  geom_point(mapping= aes(x=trans, y = hwy, color = displ < 5))
```

![plot of chunk unnamed-chunk-26](figure/unnamed-chunk-26-1.png)

Becomes a boolean 

3.5 Facets

To split into subplots, categorical variables
facet_wrap(~ <VARIABLE>)


```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)
```

![plot of chunk unnamed-chunk-27](figure/unnamed-chunk-27-1.png)

Can facet by two variables 
facet_grid(<VARIABLE1> ~ <VARIABLE2>)

```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_grid(drv ~ cyl)
```

![plot of chunk unnamed-chunk-28](figure/unnamed-chunk-28-1.png)

####3.5.1 Exercises
1. What happens if facet on a continuous variable?

```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ hwy)
```

![plot of chunk unnamed-chunk-29](figure/unnamed-chunk-29-1.png)
Makes each number in continuous variable into discrete category

2. What do the empty cells in plot with facet_grid(drv ~ cyl) mean? How do they relate to this plot?


```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = drv, y = cyl))
```

![plot of chunk unnamed-chunk-30](figure/unnamed-chunk-30-1.png)


```r
ggplot(data = mpg) + geom_point(mapping = aes(x=drv, y=cyl)) + facet_grid(drv~cyl)
```

![plot of chunk unnamed-chunk-31](figure/unnamed-chunk-31-1.png)
Empty cells mean there is not data point for that coordinate of drv, cyl. The empty cells relate to the absence of data point in that coordinate.

3. What plots does the following code make? What does . do?


```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)
```

![plot of chunk unnamed-chunk-32](figure/unnamed-chunk-32-1.png)

```r
## scatterplot of displ versus hwy, faceted based on wheel drive

ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)
```

![plot of chunk unnamed-chunk-32](figure/unnamed-chunk-32-2.png)

```r
## scatterplot of disp versus hwy, faceted based on # of cyl
```

The . prevents faceting in row or columns dimension when faceting. From ?facet_grid: "the dot in the formula is used to indicate there should be no faceting on this dimension (either row or column)."


```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_wrap(~ cyl)
```

![plot of chunk unnamed-chunk-33](figure/unnamed-chunk-33-1.png)

but how is it different from below: if you ommit the .

```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(~ cyl)
```

![plot of chunk unnamed-chunk-34](figure/unnamed-chunk-34-1.png)

4. What are the advantages to using faceting instead of the colour aesthetic? What are the disadvantages? How might the balance change if you had a larger dataset?


```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)
```

![plot of chunk unnamed-chunk-35](figure/unnamed-chunk-35-1.png)

Adv: Less crowded, can look at data separated by subsetting
Dis: Taken away from whole, hard to see how different subsets of data might be driving whole data trends
More faceting as dataset gets larger

5. Read ?facet_wrap

```r
?facet_wrap
```

nrow indicate number of rows for facets
ncol indicate number of cols for facets

facet_grid doesn't have nrow or ncol variables because that's pre-defined in the facetting variables for facets 

6. When using facet_grid() you should usually put the variable with more unique levels in the columns. Why?

Better use of screen space. Computer screens wider than they are tall.
