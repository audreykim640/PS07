README.Rmd
================

``` r
library(tidyverse)
library(openintro)
library(ggplot2)
```

# Bechdel Test vs. Time Plots

Tip: RStudio menu bar -&gt; Help -&gt; Markdown Quick Reference for
markdown formatting tips

### Establishing Dataframe

For SDS220 (Intro Probability/Stats) class, my final project group
looked at data regarding the Bechdel test sourced from FiveThirtyEight.

``` r
movies_og <- read.csv("movies.csv")

# I noticed that the domgross and intgross variables are factors, so this changes them into quantitative variables so that we can apply mathematical operations. 
# Dataframe "movies_og" is the data from the csv file, but "movies" is what I'll be working with.
movies <- movies_og %>%  
  mutate(domgross = as.numeric(as.character(domgross)), intgross = as.numeric(as.character(intgross)))
```

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

## Some pretty plots!

These plots are from some data exploration I conducted for the project.
They didn’t make it into the final project, but I still enjoy them.

``` r
fiveprops_by_year <- movies %>%
  group_by(year) %>%
  count(clean_test) %>%
mutate(fiveprops = n/sum(n))

p_fiveprops <- ggplot(fiveprops_by_year, aes(x=year, y=fiveprops, fill=clean_test)) + 
  geom_bar(position="stack", stat="identity")
p_fiveprops + labs(title="Proportions of Bechdel Test Statuses throughout Time", x="Year", y="Proportions", fill="Status")
```

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
p_fivenums <- ggplot(fiveprops_by_year, aes(x=year, y=n, fill=clean_test)) + 
  geom_bar(position="stack", stat="identity")
p_fivenums + labs(title="Bechdel Test Statuses throughout Time", x="Year", y="Number of Movies", fill="Status")
```

![](README_files/figure-gfm/unnamed-chunk-2-2.png)<!-- -->
