R Notebook for beetle data
================

  - [The data set](#the-data-set)
      - [Flour beetle](#flour-beetle)
          - [The source of the dataset](#the-source-of-the-dataset)
  - [Variables](#variables)
      - [Libraries](#libraries)
      - [Plots](#plots)

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you
execute code within the notebook, the results appear beneath the code.

# The data set

This data set the mortality of flour beetles (Tribolium confusum) after
exposure to carbon disulfide gas for 5 hours.

## Flour beetle

![Flour Beetle](Graphics/Red-flour-beetle.jpg)

Source:
<https://plunketts.net/pest-identification/other-pests/red-flour-beetles-confused-flour-beetles>

### The source of the dataset

Burnham, K. P., Anderson, D. R. (2002) Model Selection and Multimodel
Inference: a practical information-theoretic approach. Second edition.
Springer: New York.

Young, L. J., Young, J. H. (1998) Statistical Ecology. Kluwer Academic
Publishers: London.

# Variables

We have chosen to use the following naming convention: lower case words
seperated by \_ in the case of variables, and first word lowercase and
any additional words in upper case for functions. An example of a
variable structured via this naming convention might be weight\_kg, and
an example of a properly named function would be computeAverage.

``` r
beetle_data <- read.csv("Data/beetle.csv")
str(beetle_data)
```

    ## 'data.frame':    8 obs. of  4 variables:
    ##  $ dose_mg       : num  49.1 53 56.9 60.8 64.8 ...
    ##  $ number_tested : int  49 60 62 56 63 59 62 60
    ##  $ number_killed : int  6 13 18 28 52 53 61 60
    ##  $ mortality_rate: num  0.122 0.217 0.29 0.5 0.825 ...

## Libraries

``` r
library(ggplot2)
library(tidyverse)
```

## Plots

``` r
beetle_data %>%
  ggplot(aes(x = dose_mg, y = mortality_rate)) +
    geom_point() +
    geom_smooth(method = 'lm')
```

    ## `geom_smooth()` using formula 'y ~ x'

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

Now let’s compute if statistics verify the positive correlation between
the dose and the mortality rate. The method between two continuous
variables can be computed using a pearson correlation.

``` r
x = beetle_data$dose_mg
y = beetle_data$mortality_rate
cor(x,y, method = "pearson")
```

    ## [1] 0.9713805

As might have been expected, the correlation between both variables is
strong.
