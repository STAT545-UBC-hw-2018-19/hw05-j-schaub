Homework 5: Factor and Figure Management
================
Jessica Schaub
October 10, 2018

-   [Introduction](#introduction)
-   [Load Packages](#load-packages)

### Introduction

For this assignment, we will refine our figure-making skills and learn to work with factors. We are given the option of working with `Gapminder` or `Singer` datasets, and I have chosen `Gapminder`. Please see the [assignment](http://stat545.com/Classroom/assignments/hw05/hw05.html) for more information.

### Load Packages

The required packages for this assignment are loaded here.

``` r
# tidyverse
suppressPackageStartupMessages(library(tidyverse))
# knitr
suppressPackageStartupMessages(library(knitr))
#gapminder
suppressPackageStartupMessages(library(gapminder))
```

#### Part 1: Factor Management

The task here is to determine whether all variables are factors, then to (i) drop factors and (ii) Reorder levels based on knowledge from data.

It is helpful to define the following terms: - factor: Used to represent categorical data. They are stored as integers but look and behave like characters - level: A pre-defined set of values that a factor can contain. - Ex. "Male" & "Female" are two levels for the factor "Gender"

##### Characterize the Data Before Manipulation

Before performing our manipulations, we must determine what type of data we are using.

``` r
#Check gapminder variable types
sapply(gapminder, class)
```

    ##   country continent      year   lifeExp       pop gdpPercap 
    ##  "factor"  "factor" "integer" "numeric" "integer" "numeric"

It seems only the "Continent" and "Country" variables are factors, so we will work with these variables in our manipulation.

##### Drop Oceania

The task is now to remove all observations of Oceania from the data frame, then remove unused factor levels.

``` r
# Remove Oceania
gap_no_oceania <- gapminder %>% 
  filter(continent != "Oceania")
```

Now that we have removed Oceania, we can check number of rows to determine if it worked.

``` r
# How many observations of Oceania were present in the original data set
nrow(gapminder[gapminder$continent == "Oceania",])
```

    ## [1] 24

``` r
# Check data frame dimensions
nrow(gapminder)  #original
```

    ## [1] 1704

``` r
nrow(gap_no_oceania)   #removed Oceania
```

    ## [1] 1680

There were 24 observations of Oceania in the original Gapminder data set, and the new data set has lost 24 rows. Our removal worked!

Now we can check if we have unused levels.

``` r
ggplot(gap_no_oceania, aes(continent)) +
  geom_bar() +
  scale_x_discrete(drop = FALSE)
```

![](homework5_schaub_files/figure-markdown_github/unnamed-chunk-5-1.png)

The levels of Oceania still exist! We should remove the unused levels.

``` r
#Remove unused levels
gap_no_oceania <- droplevels(gap_no_oceania)
```

Then we can check if it worked.

``` r
ggplot(gap_no_oceania, aes(continent)) +
  geom_bar() +
  scale_x_discrete(drop = FALSE)
```

![](homework5_schaub_files/figure-markdown_github/unnamed-chunk-7-1.png)

It worked!

##### Reorder the Levels of `Country` or `Continent`

In this section, I will reorder the levels of country by population, from highest to lowest.

``` r
ggplot(gapminder, aes(country, pop)) +
  geom_boxplot() +
  scale_y_log10() +
  xlab("Country") +
  ylab("Population") +
  ggtitle("Population of the World's Countries") +
  theme(axis.text.x = element_text(angle = 90, hjust = 1, size = 5))
```

![](homework5_schaub_files/figure-markdown_github/unnamed-chunk-8-1.png)

##### Characterize the Data After Manipulation

##### Observations

1.  2.  3.  

#### Part 2: File I/O

##### Experimenting with `read_csv()/write_csv()`

In this section, we must create a new data set by writing data to a csv file using `write_csv()` and then read it back in using `read_csv`. I

##### Visualizing the New Data

##### Observations

1.  2.  3.  

#### Part 3: Visualization Design

##### New Figure

##### Plotly Graph

##### Observations

1.  2.  3.  

#### Part 4: Writing Figures to File

##### Use `ggsave()`

##### Load and Embed Figure

##### Observations

1.  2.  3.
