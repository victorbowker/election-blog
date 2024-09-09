---
title: Blog Post 1
author: Victor Bowker
date: '2024-09-08'
slug: blog-post-1
categories: []
tags: []
---
Hello all! I am so excited to begin on this journey of forecasting the 2024 Presidential Election. Please understand that this will be updated often, and I have no guarantee that this projection will be correct! Thanks for reading - VB


_Past Vote Share - Overall_

One of the more critical aspects of forecasting is understanding the past. Data can be an incredible tool in understanding past elections, will will allow us to predict the next ones. 



my_custom_theme <- 
  theme_bw() + 
  theme(panel.border = element_blank(),
        plot.title = element_text(size = 15, hjust = 0.5), 
        axis.text.x = element_text(angle = 45, hjust = 1),
        axis.text = element_text(size = 12),
        strip.text = element_text(size = 18),
        axis.line = element_line(colour = "black"),
        legend.position = "top",
        legend.text = element_text(size = 12))


```r
my_custom_theme <-
  theme_minimal() +
  theme(axis.text = element_text(size = 8),
        strip.text = element_text(size = 13),
          )
```









<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="672" />

| year|party      |winner |candidate          |       pv|     pv2p|incumbent |incumbent_party |prev_admin |
|----:|:----------|:------|:------------------|--------:|--------:|:---------|:---------------|:----------|
| 1948|democrat   |TRUE   |Truman, Harry      | 49.50723| 52.31764|TRUE      |TRUE            |FALSE      |
| 1948|republican |FALSE  |Dewey, Thomas      | 45.12095| 47.68236|FALSE     |FALSE           |FALSE      |
| 1952|democrat   |FALSE  |Stevenson, Adlai   | 44.37788| 44.71056|FALSE     |TRUE            |FALSE      |
| 1952|republican |TRUE   |Eisenhower, Dwight | 54.87805| 55.28944|FALSE     |FALSE           |FALSE      |
| 1956|democrat   |FALSE  |Stevenson, Adlai   | 41.95397| 42.23566|TRUE      |FALSE           |FALSE      |
| 1956|republican |TRUE   |Eisenhower, Dwight | 57.37908| 57.76434|TRUE      |TRUE            |FALSE      |
| 1960|republican |FALSE  |Nixon, Richard M.  | 49.54829| 49.91324|FALSE     |TRUE            |TRUE       |
| 1960|democrat   |TRUE   |Kennedy, John F.   | 49.72054| 50.08676|FALSE     |FALSE           |FALSE      |
| 1964|republican |FALSE  |Goldwater, Barry   | 38.47172| 38.65603|FALSE     |FALSE           |FALSE      |
| 1964|democrat   |TRUE   |Johnson, Lyndon B. | 61.05148| 61.34397|TRUE      |TRUE            |TRUE       |
| 1968|republican |TRUE   |Nixon, Richard M.  | 43.41574| 50.40462|FALSE     |FALSE           |TRUE       |
| 1968|democrat   |FALSE  |Humphrey, Hubert   | 42.71871| 49.59538|FALSE     |TRUE            |FALSE      |
| 1972|republican |TRUE   |Nixon, Richard M.  | 60.69324| 61.78901|TRUE      |TRUE            |TRUE       |
| 1972|democrat   |FALSE  |McGovern, George   | 37.53336| 38.21099|FALSE     |FALSE           |FALSE      |
| 1976|democrat   |TRUE   |Carter, Jimmy      | 49.85267| 51.13735|FALSE     |FALSE           |FALSE      |
| 1976|republican |FALSE  |Ford, Gerald       | 47.63511| 48.86265|TRUE      |TRUE            |TRUE       |
| 1980|democrat   |FALSE  |Carter, Jimmy      | 41.01993| 44.84244|TRUE      |TRUE            |FALSE      |
| 1980|republican |TRUE   |Reagan, Ronald     | 50.45575| 55.15756|FALSE     |FALSE           |FALSE      |
| 1984|democrat   |FALSE  |Mondale, Walter    | 40.41862| 40.87665|FALSE     |FALSE           |TRUE       |
| 1984|republican |TRUE   |Reagan, Ronald     | 58.46086| 59.12335|TRUE      |TRUE            |FALSE      |
| 1988|democrat   |FALSE  |Dukakis, Michael   | 45.54878| 46.16754|FALSE     |FALSE           |FALSE      |
| 1988|republican |TRUE   |Bush, George H.W.  | 53.11096| 53.83246|FALSE     |TRUE            |TRUE       |
| 1992|democrat   |TRUE   |Clinton, Bill      | 42.88417| 53.62070|FALSE     |FALSE           |FALSE      |
| 1992|republican |FALSE  |Bush, George H.W.  | 37.09273| 46.37930|TRUE      |TRUE            |TRUE       |
| 1996|democrat   |TRUE   |Clinton, Bill      | 49.06675| 54.80402|TRUE      |TRUE            |FALSE      |
| 1996|republican |FALSE  |Dole, Robert       | 40.46454| 45.19598|FALSE     |FALSE           |FALSE      |
| 2000|democrat   |FALSE  |Gore, Al           | 48.14325| 50.25952|FALSE     |TRUE            |TRUE       |
| 2000|republican |TRUE   |Bush, George W.    | 47.64606| 49.74048|FALSE     |FALSE           |FALSE      |
| 2004|democrat   |FALSE  |Kerry, John        | 48.06646| 48.73068|FALSE     |FALSE           |FALSE      |
| 2004|republican |TRUE   |Bush, George W.    | 50.57049| 51.26932|TRUE      |TRUE            |FALSE      |
| 2008|democrat   |TRUE   |Obama, Barack H.   | 52.76156| 53.77077|FALSE     |FALSE           |FALSE      |
| 2008|republican |FALSE  |McCain, John       | 45.36157| 46.22923|FALSE     |TRUE            |FALSE      |
| 2012|democrat   |TRUE   |Obama, Barack H.   | 50.87488| 51.91526|TRUE      |TRUE            |TRUE       |
| 2012|republican |FALSE  |Romney, Mitt       | 47.12113| 48.08474|FALSE     |FALSE           |FALSE      |
| 2016|democrat   |FALSE  |Clinton, Hillary   | 47.05731| 51.16249|FALSE     |TRUE            |TRUE       |
| 2016|republican |TRUE   |Trump, Donald J.   | 44.91888| 48.83751|FALSE     |FALSE           |FALSE      |
| 2020|democrat   |TRUE   |Biden, Joseph R.   | 51.31571| 52.26986|FALSE     |FALSE           |FALSE      |
| 2020|republican |FALSE  |Trump, Donald J.   | 46.85886| 47.73014|TRUE      |TRUE            |TRUE       |











<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-14-1.png" width="672" />


```
## Warning in left_join(filter(d_pvstate_wide, year >= 1980), states_map, by = "region"): Detected an unexpected many-to-many relationship between `x` and `y`.
## ℹ Row 1 of `x` matches multiple rows in `y`.
## ℹ Row 1 of `y` matches multiple rows in `x`.
## ℹ If a many-to-many relationship is expected, set `relationship =
##   "many-to-many"` to silence this warning.
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-15-1.png" width="672" />








```
## Warning: Removed 12 rows containing missing values (`geom_text()`).
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-20-1.png" width="672" />








