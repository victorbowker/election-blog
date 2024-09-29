---
title: Blog Post 4
author: Victor Bowker
date: '2024-09-28'
slug: blog-4
categories: []
tags: []
---

**Welcome**
Hello and thank you for coming back to another week of election predictions! This week, I am primarily focusing on incumbency, and the impacts it can have on an election. In general ways, incumbents are given _a lot_ of advantages. This can make it very difficult for new, emerging canddiates to get a foothold in the race, lending an explanation to usually over 90% of all Congressional incumbents winning their re-election bids.[1]

First, lets talk about why it is so easy for incumbents to win re-election. Simply put, their status as an incumbent can be incredibly helpful. Constituents are already familiar with the candidate's positions and track record. Additionally, there is a feeling of comfort with familiarity, meaning unless an incumbent committed an atrocity, its likely they will be re-elected [2]

When you consider Political Action Committees, which funnel financial support to candidates, the picture becomes even clearer. There is a cycle of support from a PAC, then a Congressman does them favors (or simply votes as they would, coincidentally aligning with PAC views) by voting on bills, then the PAC gives more money. [3]

So, you may wonder, could we just make a prediction that nearly all of Congress will win re-election (if they seek it) and there is a pretty good chance that the President will win? NO!

That would simply be too easy--and ignoring too much information. We have seen many times where candidates lost as incumbents, like George H. W. Bush or Donald Trump. Additionally, there are many factors still at play that would be neglected if we simply look at past results. One example, which I looked into in past weeks, is the economy, where Goldman Sachs Political Economists have found that incumbents lose at higher rates during

# Load libraries.
## install via `install.packages("name")`
library(viridis)
library(sf)


```r
library(car)
```

```
## Loading required package: carData
```

```r
library(caret)
```

```
## Loading required package: ggplot2
```

```
## Loading required package: lattice
```

```r
library(CVXR)
```

```
## Warning: package 'CVXR' was built under R version 4.3.3
```

```
## 
## Attaching package: 'CVXR'
```

```
## The following object is masked from 'package:stats':
## 
##     power
```

```r
library(glmnet)
```

```
## Loading required package: Matrix
```

```
## Loaded glmnet 4.1-8
```

```r
library(kableExtra)
library(maps)
library(RColorBrewer)
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.3     ✔ readr     2.1.4
## ✔ forcats   1.0.0     ✔ stringr   1.5.0
## ✔ lubridate 1.9.2     ✔ tibble    3.2.1
## ✔ purrr     1.0.2     ✔ tidyr     1.3.0
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ tidyr::expand()     masks Matrix::expand()
## ✖ dplyr::filter()     masks stats::filter()
## ✖ dplyr::group_rows() masks kableExtra::group_rows()
## ✖ dplyr::id()         masks CVXR::id()
## ✖ purrr::is_vector()  masks CVXR::is_vector()
## ✖ dplyr::lag()        masks stats::lag()
## ✖ purrr::lift()       masks caret::lift()
## ✖ purrr::map()        masks maps::map()
## ✖ tidyr::pack()       masks Matrix::pack()
## ✖ dplyr::recode()     masks car::recode()
## ✖ purrr::some()       masks car::some()
## ✖ tidyr::unpack()     masks Matrix::unpack()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```
## set working directory here
# setwd("~")

####----------------------------------------------------------#
#### Read, merge, and process data.
####----------------------------------------------------------#

```r
# Read incumbency/vote data.
d_vote <- read_csv("popvote_1948-2020.csv")
```

```
## Rows: 40 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): party, candidate
## dbl (5): year, pv, pv2p, deminc, juneapp
## lgl (4): winner, incumbent, incumbent_party, prev_admin
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
d_state_vote <- read_csv("state_popvote_1948_2020.csv")
```

```
## Rows: 959 Columns: 14
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): state
## dbl (13): year, D_pv, R_pv, D_pv2p, R_pv2p, D_pv_lag1, R_pv_lag1, D_pv2p_lag...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
d_vote$party[d_vote$party == "democrat"] <- "DEM"
d_vote$party[d_vote$party == "republican"] <- "REP"
```


```r
# Read economic data.
d_econ <- read_csv("fred_econ.csv") |> 
  filter(quarter == 2)
```

```
## Rows: 387 Columns: 14
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (14): year, quarter, GDP, GDP_growth_quarterly, RDPI, RDPI_growth_quarte...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
# Read polling and election results data. 
d_pollav_natl <- read_csv("national_polls_1968-2024.csv")
```

```
## Rows: 7378 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (3): state, party, candidate
## dbl  (4): year, weeks_left, days_left, poll_support
## lgl  (1): before_convention
## date (1): poll_date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
d_pollav_state <- read_csv("state_polls_1968-2024.csv")
```

```
## Rows: 204564 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (3): state, party, candidate
## dbl  (4): year, weeks_left, days_left, poll_support
## lgl  (1): before_convention
## date (1): poll_date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
# Shape and merge polling and election data using November polls. 
d_poll_nov <- d_vote |> 
  left_join(d_pollav_natl |> 
              group_by(year, party) |> 
              top_n(1, poll_date) |> 
              select(-candidate), 
            by = c("year", "party")) |> 
  rename(nov_poll = poll_support) |> 
  filter(year <= 2020) |> 
  drop_na()
```


```r
# Create dataset of polling average by week until the election. 
d_poll_weeks <- d_pollav_natl |> 
  group_by(year, party, weeks_left) |>
  summarize(mean_poll_week = mean(poll_support)) |> 
  filter(weeks_left <= 30) |> 
  pivot_wider(names_from = weeks_left, values_from = mean_poll_week) |> 
  left_join(d_vote, by = c("year", "party"))
```

```
## `summarise()` has grouped output by 'year', 'party'. You can override using the
## `.groups` argument.
```

####----------------------------------------------------------#
#### Descriptive statistics on the incumbency advantage. 
####----------------------------------------------------------#


```r
# How many post-war elections (18 and 2024) have there been 
# where an incumbent president won? 
d_vote |> 
  filter(winner) |> 
  select(year, win_party = party, win_cand = candidate) |> 
  mutate(win_party_last = lag(win_party, order_by = year),
         win_cand_last = lag(win_cand, order_by = year)) |> 
  mutate(reelect_president = win_cand_last == win_cand) |> 
  filter(year > 1948 & year < 2024) |> 
  group_by(reelect_president) |> 
  summarize(N = n()) |> 
  mutate(Percent = round(N/sum(N) * 100, 2)) |>
  as.data.frame()
```

```
##   reelect_president  N Percent
## 1             FALSE 12   66.67
## 2              TRUE  6   33.33
```


```r
# A different way of assessing the incumbency advantage 
# (out of 11 elections where there was at least one incumbent running). 
inc_tab <- d_vote |> 
  filter(year > 1948 & year < 2024) |>
  select(year, party, candidate, incumbent, winner) |> 
  pivot_wider(names_from = party, 
              values_from = c(candidate, incumbent, winner)) |> 
  filter(incumbent_DEM == TRUE | incumbent_REP == TRUE)


cat(paste0("Elections with At Least One Incumbent Running: ", nrow(inc_tab), "\n",
   "Incumbent Victories: ", (sum(inc_tab$incumbent_REP & inc_tab$winner_REP) + 
                             sum(inc_tab$incumbent_DEM & inc_tab$winner_DEM)), "\n",
    "Percentage: ", round((sum(inc_tab$incumbent_REP & inc_tab$winner_REP) + 
                           sum(inc_tab$incumbent_DEM & inc_tab$winner_DEM))/
                           nrow(inc_tab)*100, 2)))
```

```
## Elections with At Least One Incumbent Running: 11
## Incumbent Victories: 7
## Percentage: 63.64
```


```r
# In the six elections since 2000?
inc_tab |> 
  filter(year >= 2000)
```

```
## # A tibble: 3 × 7
##    year candidate_DEM    candidate_REP    incumbent_DEM incumbent_REP winner_DEM
##   <dbl> <chr>            <chr>            <lgl>         <lgl>         <lgl>     
## 1  2004 Kerry, John      Bush, George W.  FALSE         TRUE          FALSE     
## 2  2012 Obama, Barack H. Romney, Mitt     TRUE          FALSE         TRUE      
## 3  2020 Biden, Joseph R. Trump, Donald J. FALSE         TRUE          TRUE      
## # ℹ 1 more variable: winner_REP <lgl>
```


```r
# How many post-war elections have there been where the incumbent *party* won? 
d_vote |> 
  filter(winner) |> 
  select(year, win_party = party, win_cand = candidate) |> 
  mutate(win_party_last = lag(win_party, order_by = year),
         win_cand_last = lag(win_cand, order_by = year)) |> 
  mutate(reelect_party = win_party_last == win_party) |> 
  filter(year > 1948 & year < 2024) |> 
  group_by(reelect_party) |> 
  summarize(N = n()) |> 
  mutate(Percent = round(N/sum(N) * 100, 2)) |>
  as.data.frame()
```

```
##   reelect_party  N Percent
## 1         FALSE 10   55.56
## 2          TRUE  8   44.44
```


```r
# How many post-war elections have there been where winner served in 
# previous administration?
100*round(prop.table(table(`prev_admin` = d_vote$prev_admin[d_vote$year > 1948 & 
                                     d_vote$year < 2024 & 
                                     d_vote$winner == TRUE])), 4)
```

```
## prev_admin
## FALSE  TRUE 
## 72.22 27.78
```
####----------------------------------------------------------#
#### Pork analysis. 
####----------------------------------------------------------#

```r
# Read federal grants dataset from Kriner & Reeves (2008). 
d_pork_state <- read_csv("fedgrants_bystate_1988-2008.csv")
```

```
## Rows: 1251 Columns: 7
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (3): state_abb, state_year_type, state_year_type2
## dbl (4): year, elxn_year, grant_mil, state_incvote_avglast3
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
# What strategy do presidents pursue? 
d_pork_state |> 
  filter(!is.na(state_year_type)) |> 
  group_by(state_year_type) |>
  summarize(mean_grant = mean(grant_mil, na.rm = T), se_grant = sd(grant_mil, na.rm = T)/sqrt(n())) |> 
  ggplot(aes(x = state_year_type, y = mean_grant, ymin = mean_grant-1.96*se_grant, ymax = mean_grant+1.96*se_grant)) + 
  coord_flip() + 
  geom_bar(stat = "identity", fill = "chartreuse4") + 
  geom_errorbar(width = 0.2) + 
  labs(x = "Type of State & Year", 
       y = "Federal Grant Spending (Millions of $)", 
       title = "Federal Grant Spending (Millions $) by State Election Type") + 
  theme_minimal() + 
  theme(plot.title = element_text(size = 20),
        axis.title = element_text(size = 15),
        axis.text = element_text(size = 12))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-13-1.png" width="672" />


```r
# Do presidents strategize for their successor as well? 
d_pork_state |> 
  filter(!is.na(state_year_type2)) |> 
  group_by(state_year_type2) |>
  summarize(mean_grant = mean(grant_mil, na.rm = T), se_grant = sd(grant_mil, na.rm = T)/sqrt(n())) |> 
  ggplot(aes(x = state_year_type2, y = mean_grant, ymin = mean_grant-1.96*se_grant, ymax = mean_grant+1.96*se_grant)) + 
  coord_flip() + 
  geom_bar(stat = "identity", fill = "chartreuse4") + 
  geom_errorbar(width = 0.2) + 
  labs(x = "Type of State & Year", 
       y = "Federal Grant Spending (Millions of $)", 
       title = "Federal Grant Spending (Millions $) by State Election Type") + 
  theme_minimal() +
  theme(plot.title = element_text(size = 20),
        axis.title = element_text(size = 15),
        axis.text = element_text(size = 12))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-14-1.png" width="672" />


```r
# Pork county model. 
d_pork_county <- read_csv("fedgrants_bycounty_1988-2008.csv")
```

```
## Rows: 18465 Columns: 16
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (3): state, county, state_abb
## dbl (13): year, state_FIPS, county_FIPS, dvoteswing_inc, dpct_grants, dpc_in...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
pork_mod_county_1 <- lm(dvoteswing_inc  ~ dpct_grants*comp_state + as.factor(year), 
                      d_pork_county)
summary(pork_mod_county_1)
```

```
## 
## Call:
## lm(formula = dvoteswing_inc ~ dpct_grants * comp_state + as.factor(year), 
##     data = d_pork_county)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -27.7179  -2.8547  -0.0047   2.7889  23.2187 
## 
## Coefficients:
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)            -6.450079   0.084452 -76.376  < 2e-16 ***
## dpct_grants             0.004762   0.001036   4.595 4.35e-06 ***
## comp_state              0.152687   0.076143   2.005 0.044949 *  
## as.factor(year)1992     0.170688   0.115787   1.474 0.140458    
## as.factor(year)1996     6.345396   0.115509  54.934  < 2e-16 ***
## as.factor(year)2000    -2.049544   0.116215 -17.636  < 2e-16 ***
## as.factor(year)2004     8.407388   0.115576  72.743  < 2e-16 ***
## as.factor(year)2008     3.136792   0.116122  27.013  < 2e-16 ***
## dpct_grants:comp_state  0.006391   0.001764   3.623 0.000292 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.495 on 18455 degrees of freedom
##   (1 observation deleted due to missingness)
## Multiple R-squared:  0.4027,	Adjusted R-squared:  0.4025 
## F-statistic:  1556 on 8 and 18455 DF,  p-value: < 2.2e-16
```

```r
pork_mod_county_2 <- lm(dvoteswing_inc ~ dpct_grants*comp_state + as.factor(year) +
                          dpc_income + inc_ad_diff + inc_campaign_diff + 
                          dhousevote_inc + iraq_cas2004 + iraq_cas2008 + 
                          dpct_popl,
                        data = d_pork_county)
summary(pork_mod_county_2)
```

```
## 
## Call:
## lm(formula = dvoteswing_inc ~ dpct_grants * comp_state + as.factor(year) + 
##     dpc_income + inc_ad_diff + inc_campaign_diff + dhousevote_inc + 
##     iraq_cas2004 + iraq_cas2008 + dpct_popl, data = d_pork_county)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -27.321  -2.848  -0.025   2.728  22.994 
## 
## Coefficients:
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)            -6.523210   0.084963 -76.777  < 2e-16 ***
## dpct_grants             0.003954   0.001043   3.792 0.000150 ***
## comp_state              0.155418   0.077223   2.013 0.044173 *  
## as.factor(year)1992    -0.156389   0.120591  -1.297 0.194699    
## as.factor(year)1996     6.230500   0.119533  52.124  < 2e-16 ***
## as.factor(year)2000    -2.000293   0.118588 -16.868  < 2e-16 ***
## as.factor(year)2004     8.248378   0.119371  69.099  < 2e-16 ***
## as.factor(year)2008     3.574248   0.124060  28.811  < 2e-16 ***
## dpc_income              0.134285   0.022326   6.015 1.84e-09 ***
## inc_ad_diff             0.061345   0.010851   5.654 1.60e-08 ***
## inc_campaign_diff       0.161845   0.013166  12.292  < 2e-16 ***
## dhousevote_inc          0.012093   0.001952   6.196 5.91e-10 ***
## iraq_cas2004           -0.153092   0.069585  -2.200 0.027816 *  
## iraq_cas2008           -0.164783   0.021677  -7.602 3.07e-14 ***
## dpct_popl               2.103344   0.530292   3.966 7.33e-05 ***
## dpct_grants:comp_state  0.006411   0.001781   3.600 0.000319 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.452 on 17943 degrees of freedom
##   (506 observations deleted due to missingness)
## Multiple R-squared:  0.4199,	Adjusted R-squared:  0.4194 
## F-statistic: 865.9 on 15 and 17943 DF,  p-value: < 2.2e-16
```


```r
# Pork state model. 
d_pork_state_model <- d_state_vote |>
  mutate(state_abb = state.abb[match(d_state_vote$state, state.name)]) |>
  inner_join(d_pork_state, by = c("year", "state_abb")) |>
  left_join(d_vote, by = "year") |>
  filter(incumbent_party == TRUE) |>
  mutate(inc_pv2p = ifelse(party == "REP", R_pv2p, D_pv2p)) |>
  mutate(is_comp = case_when(state_year_type == "swing + election year" ~ 1,
                             .default = 0)) |>
  group_by(state) |>
  mutate(change_grant_mil = (1-grant_mil/(lag(grant_mil, n = 1)))*100,
         change_inc_pv2p = (1-inc_pv2p/(lag(inc_pv2p, n = 1)))*100) |>
  ungroup() |>
  select(state, year, is_comp, change_grant_mil, change_inc_pv2p)
```

```
## Warning in left_join(inner_join(mutate(d_state_vote, state_abb = state.abb[match(d_state_vote$state, : Detected an unexpected many-to-many relationship between `x` and `y`.
## ℹ Row 1 of `x` matches multiple rows in `y`.
## ℹ Row 19 of `y` matches multiple rows in `x`.
## ℹ If a many-to-many relationship is expected, set `relationship =
##   "many-to-many"` to silence this warning.
```

```r
pork_state_mod <- lm(change_inc_pv2p ~ is_comp*change_grant_mil + as.factor(year),
                     data = d_pork_state_model)
summary(pork_state_mod)
```

```
## 
## Call:
## lm(formula = change_inc_pv2p ~ is_comp * change_grant_mil + as.factor(year), 
##     data = d_pork_state_model)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -136.740   -6.628    0.341    7.176   64.748 
## 
## Coefficients:
##                          Estimate Std. Error t value Pr(>|t|)    
## (Intercept)                9.6346     3.6317   2.653  0.00842 ** 
## is_comp                   -0.4004     4.1498  -0.096  0.92319    
## change_grant_mil           0.1138     0.1051   1.082  0.28001    
## as.factor(year)1992        6.8952     6.7168   1.027  0.30548    
## as.factor(year)1996      -21.3789     5.2732  -4.054 6.46e-05 ***
## as.factor(year)2000        3.5773     5.6260   0.636  0.52537    
## as.factor(year)2004      -30.1619     5.4753  -5.509 7.96e-08 ***
## as.factor(year)2008        1.0850     4.8627   0.223  0.82360    
## is_comp:change_grant_mil  -0.1027     0.1643  -0.625  0.53246    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 23.43 on 291 degrees of freedom
##   (50 observations deleted due to missingness)
## Multiple R-squared:  0.2675,	Adjusted R-squared:  0.2474 
## F-statistic: 13.29 on 8 and 291 DF,  p-value: 2.299e-16
```
####----------------------------------------------------------#
#### Time for a change model. 
####----------------------------------------------------------#


```r
# Join data for time for change model.
d_tfc_train <- d_vote |> 
  left_join(d_econ, by = "year") |> 
  filter(incumbent_party) |>
  mutate(incumbent = as.numeric(incumbent))
```


```r
# Estimate time for change model through 2016.
tfc_mod_2016 <- lm(pv2p ~ GDP_growth_quarterly + incumbent + juneapp, 
                   data = subset(d_tfc_train, year < 2020))
summary(tfc_mod_2016)
```

```
## 
## Call:
## lm(formula = pv2p ~ GDP_growth_quarterly + incumbent + juneapp, 
##     data = subset(d_tfc_train, year < 2020))
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -3.8593 -1.1826 -0.2782  1.7858  3.9544 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          48.21244    1.06959  45.076  < 2e-16 ***
## GDP_growth_quarterly  0.46505    0.15494   3.001 0.009523 ** 
## incumbent             2.22003    1.24448   1.784 0.096122 .  
## juneapp               0.13177    0.02514   5.241 0.000125 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.486 on 14 degrees of freedom
## Multiple R-squared:  0.8166,	Adjusted R-squared:  0.7773 
## F-statistic: 20.78 on 3 and 14 DF,  p-value: 2.007e-05
```

```r
# Estimate simplified time for change model for 2020. 
# https://www-cambridge-org.ezp-prod1.hul.harvard.edu/core/services/aop-cambridge-core/content/view/47BBC0D5A2B7913DBB37FDA0542FD7E8/S1049096520001389a.pdf/its-the-pandemic-stupid-a-simplified-model-for-forecasting-the-2020-presidential-election.pdf
tfc_mod_2020 <- lm(pv2p ~ juneapp, 
                   data = subset(d_tfc_train, year < 2024))
summary(tfc_mod_2020)
```

```
## 
## Call:
## lm(formula = pv2p ~ juneapp, data = subset(d_tfc_train, year < 
##     2024))
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -6.0627 -1.9331 -0.1604  1.6453  6.9681 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 51.02572    0.72026  70.844  < 2e-16 ***
## juneapp      0.16501    0.02818   5.855 1.91e-05 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.089 on 17 degrees of freedom
## Multiple R-squared:  0.6685,	Adjusted R-squared:  0.649 
## F-statistic: 34.28 on 1 and 17 DF,  p-value: 1.91e-05
```
# Evaluate models and compare them to your own models/predictions. 
# TODO: 

####----------------------------------------------------------#
#### Expert predictions. 
####----------------------------------------------------------#


```r
# Read expert prediction data. 
# Read data from Cook Political Report. 
# Years: 1988-2020
# IMPORTANT: Please do not commit/push this data to GitHub or share it anywhere outside of this course!
d_cook <- read_csv("CPR_EC_Ratings.csv")[,-1] |> 
  mutate(rating_numeric = case_when(Rating == "Solid D" ~ 1,
                                    Rating == "Likely D" ~ 2,
                                    Rating == "Lean D" ~ 3,
                                    Rating == "Toss Up" ~ 4,
                                    Rating == "Lean R" ~ 5,
                                    Rating == "Likely R" ~ 6,
                                    Rating == "Solid R" ~ 7)) |> 
  mutate(solid_D = as.numeric(rating_numeric == 1),
         likely_D = as.numeric(rating_numeric == 2),
         lean_D = as.numeric(rating_numeric == 3),
         toss_up = as.numeric(rating_numeric == 4),
         lean_R = as.numeric(rating_numeric == 5),
         likely_R = as.numeric(rating_numeric == 6),
         solid_R = as.numeric(rating_numeric == 7))
```

```
## New names:
## Rows: 474 Columns: 26
## ── Column specification
## ──────────────────────────────────────────────────────── Delimiter: "," chr
## (15): Office, Abbreviation, Rating, PluralityParty, RepCandidate, RepSta... dbl
## (6): ...1, Cycle, RepVotesMajorPercent, DemVotesMajorPercent, ThirdVote... num
## (3): RepVotes, DemVotes, PluralityVotes lgl (2): Raw, Incumbent.Party
## ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
## Specify the column types or set `show_col_types = FALSE` to quiet this message.
## • `` -> `...1`
```

```r
# N.B. Read important note above!
```


```r
# Read data from Sabato's Crystal Ball.
# Years: 2004-2024
d_sabato <- read_csv("sabato_crystal_ball_ratings.csv") |> 
  rename(state_abb = state)
```

```
## Rows: 306 Columns: 3
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (1): state
## dbl (2): year, rating
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
state_abb_xwalk <- d_state_vote |>
  mutate(state_abb = state.abb[match(d_state_vote$state, state.name)]) |> 
  select(state, state_abb) |> 
  distinct() 
state_abb_xwalk[51,]$state <- "District of Columbia"
state_abb_xwalk[51,]$state_abb <- "DC"

d_sabato <- d_sabato |> 
  left_join(state_abb_xwalk, by = "state_abb") |>
  mutate(safe_D = as.numeric(rating == 1),
         likely_D = as.numeric(rating == 2),
         lean_D = as.numeric(rating == 3),
         toss_up = as.numeric(rating == 4),
         lean_R = as.numeric(rating == 5),
         likely_R = as.numeric(rating == 6),
         safe_R = as.numeric(rating == 7))
```
# Ratings: 
# 1: Safe Democrat
# 2: Likely Democrat
# 3: Lean Democrat
# 4: Toss Up
# 5: Lean Republican
# 6: Likely Republican
# 7: Safe Republican

```r
# 2020 Comparison. 
d_sabato_2020 <- d_sabato |> 
  filter(year == 2020) |> 
  select(state, sabato_rating = rating)

d_expert_2020 <- d_cook |> 
  filter(Cycle == 2020) |> 
  select(state = State, cook_rating = rating_numeric) |> 
  left_join(d_sabato_2020, by = "state") |> 
  mutate(rating_match = as.numeric(cook_rating == sabato_rating))

d_expert_2020$rating_match |> table()
```

```
## 
##  0  1 
##  9 42
```

```r
d_expert_2020$state[d_expert_2020$rating_match == 0 & !is.na(d_expert_2020$sabato_rating)]
```

```
## [1] "Florida"        "Georgia"        "Iowa"           "Minnesota"     
## [5] "New Hampshire"  "New Mexico"     "North Carolina" "Ohio"          
## [9] "Texas"
```


```r
# Why the NAs? Cook makes ratings for Maine and Nebraska districts separately. 
# These may be important for the 2024 election, but are difficult to find data for. 

d_expert_2020 <- d_expert_2020 |> 
  drop_na()
```


```r
# Compare rating mismatches for 2020.
d_expert_2020[d_expert_2020$state %in% c(d_expert_2020$state[d_expert_2020$rating_match == 0]),]
```

```
## # A tibble: 9 × 4
##   state          cook_rating sabato_rating rating_match
##   <chr>                <dbl>         <dbl>        <dbl>
## 1 Florida                  4             5            0
## 2 Georgia                  4             3            0
## 3 Iowa                     4             5            0
## 4 Minnesota                3             2            0
## 5 New Hampshire            3             2            0
## 6 New Mexico               1             2            0
## 7 North Carolina           4             3            0
## 8 Ohio                     4             5            0
## 9 Texas                    4             5            0
```


```r
# Merge in 2020 state vote data. 
d_state_vote_2020 <- d_state_vote |> 
  filter(year == 2020) |> 
  select(state, year, R_pv2p, D_pv2p) |> 
  mutate(margin = D_pv2p - R_pv2p, 
         winner = ifelse(D_pv2p > R_pv2p, "D", "R"))
d_state_vote_2020[d_state_vote_2020$state == "District Of Columbia",]$state <- "District of Columbia"

d_expert_2020 <- d_expert_2020 |>
  left_join(d_state_vote_2020, by = "state")
```


```r
# See which expert group was more accurate for 2020 (counting toss ups as misses). 
d_expert_2020 <- d_expert_2020 |> 
  mutate(cook_correct = as.numeric((winner == "D" & cook_rating < 4) | 
                                   (winner == "R" & cook_rating > 4)),
         sabato_correct = as.numeric((winner == "D" & sabato_rating < 4) | 
                                     (winner == "R" & sabato_rating > 4)))

d_expert_2020 |>
  select(cook_correct, sabato_correct) |> 
  colMeans()
```

```
##   cook_correct sabato_correct 
##      0.8823529      0.9803922
```

```r
# Which states did Cook miss? 
d_expert_2020[d_expert_2020$cook_correct == 0,]$state
```

```
## [1] "Florida"        "Georgia"        "Iowa"           "North Carolina"
## [5] "Ohio"           "Texas"
```

```r
d_expert_2020[d_expert_2020$cook_correct == 0,] |> view()
```


```r
# Sabato? 
d_expert_2020[d_expert_2020$sabato_correct == 0,]$state
```

```
## [1] "North Carolina"
```

```r
d_expert_2020[d_expert_2020$sabato_correct == 0,] |> view()
```

# 2024 Comparison:

# 2024 toss-ups? 
# 7 from Cook: https://www.cookpolitical.com/ratings/presidential-race-ratings

# 191 EV (Solid D) + 34 (Likely D) + 1 (Lean D) = 226 EV Dem
# 93 Toss Up EV
  # 11 AZ
  # 16 GA
  # 15 MI
  # 6 NV
  # 16 NC
  # 19 PA
  # 10 WI
# 148 (Solid R) + 71 (Likely R) + 0 (Lean R) = 219 EV Rep


```r
# Sabato: 
# https://centerforpolitics.org/crystalball/2024-president/
d_sabato |> 
  filter(year == 2024 & rating == 4) |> 
  select(state)
```

```
## # A tibble: 7 × 1
##   state         
##   <chr>         
## 1 Arizona       
## 2 Georgia       
## 3 Michigan      
## 4 Nevada        
## 5 North Carolina
## 6 Pennsylvania  
## 7 Wisconsin
```
# 226 D EV
# 93 ? EV
# 219 R EV

# Conclusion: Both have same set of states as each. 
# Importance of these swing states!


```r
# Combine expert predictions generally. 
d_expert <- d_cook |> 
  select(year = Cycle, state = State, cook_rating = rating_numeric) |> 
  left_join(d_sabato |> select(year, state, sabato_rating = rating), by = c("year", "state")) |> 
  mutate(rating_match = as.numeric(cook_rating == sabato_rating)) |> 
  drop_na()

d_expert |> 
  group_by(year) |> 
  summarize(mean_match_rate = mean(rating_match)) 
```

```
## # A tibble: 5 × 2
##    year mean_match_rate
##   <dbl>           <dbl>
## 1  2004           0.647
## 2  2008           0.608
## 3  2012           0.765
## 4  2016           0.804
## 5  2020           0.824
```


```r
# Merge in voting data. 
d_state_vote_wide <- d_state_vote |> 
  select(state, year, R_pv2p, D_pv2p, R_pv2p_lag1, R_pv2p_lag2, D_pv2p_lag1, D_pv2p_lag2) |>
  mutate(margin = D_pv2p - R_pv2p, 
         winner = ifelse(D_pv2p > R_pv2p, "D", "R"))
d_state_vote_wide[d_state_vote_wide$state == "District Of Columbia",]$state <- "District of Columbia"
d_expert <- d_expert |> 
  left_join(d_state_vote_wide, 
            by = c("state", "year"))
d_expert <- d_expert |> 
  mutate(cook_correct = as.numeric((winner == "D" & cook_rating < 4) | 
                                     (winner == "R" & cook_rating > 4)),
         sabato_correct = as.numeric((winner == "D" & sabato_rating < 4) | 
                                       (winner == "R" & sabato_rating > 4)))

d_expert |>
  select(cook_correct, sabato_correct) |> 
  colMeans()
```

```
##   cook_correct sabato_correct 
##      0.8549020      0.9137255
```

```r
d_expert |> 
  group_by(year) |> 
  summarize(mean_cook_correct = mean(cook_correct),
            mean_sabato_correct = mean(sabato_correct))
```

```
## # A tibble: 5 × 3
##    year mean_cook_correct mean_sabato_correct
##   <dbl>             <dbl>               <dbl>
## 1  2004             0.824               0.961
## 2  2008             0.804               0.784
## 3  2012             0.863               0.961
## 4  2016             0.902               0.882
## 5  2020             0.882               0.980
```
# How can we incorporate expert predictions into our models? 
# TODO: 

####----------------------------------------------------------#
#### Ensembling at the national level (incumbents only).
####----------------------------------------------------------#


```r
# Split poll data into training and testing data based on inclusion or exclusion of 2024. 
d_poll_weeks_train_inc <- d_poll_weeks |> 
  filter(incumbent & year <= 2020)
d_poll_weeks_test_inc <- d_poll_weeks |> 
  filter(incumbent & year == 2024)

colnames(d_poll_weeks)[3:33] <- paste0("poll_weeks_left_", 0:30)
colnames(d_poll_weeks_train_inc)[3:33] <- paste0("poll_weeks_left_", 0:30)
colnames(d_poll_weeks_test_inc)[3:33] <- paste0("poll_weeks_left_", 0:30)
```


```r
# First check how many weeks of polling we have for 2024. 
d_pollav_natl |> 
  filter(year == 2024) |> 
  select(weeks_left) |> 
  distinct() |> 
  range() # Let's take week 30 - 7 as predictors since those are the weeks we have polling data for 2024 and historically. 
```

```
## [1]  7 36
```

```r
x.train <- d_poll_weeks_train_inc |>
  ungroup() |> 
  select(all_of(paste0("poll_weeks_left_", 7:30))) |> 
  as.matrix()
y.train <- d_poll_weeks_train_inc$pv2p
x.test <- d_poll_weeks_test_inc |>
  ungroup() |> 
  select(all_of(paste0("poll_weeks_left_", 7:30))) |> 
  as.matrix()
```


```r
# Using elastic-net for simplicity. 
set.seed(02138)
enet.poll <- cv.glmnet(x = x.train, y = y.train, alpha = 0.5)
```

```
## Warning: Option grouped=FALSE enforced in cv.glmnet, since < 3 observations per
## fold
```

```r
lambda.min.enet.poll <- enet.poll$lambda.min
```


```r
# Predict 2024 national pv2p share using elastic-net. 
(polls.pred <- predict(enet.poll, s = lambda.min.enet.poll, newx = x.test))
```

```
##            s1
## [1,] 48.71603
```


```r
# Estimate models using polls alone, fundamentals alone, and combined fundamentals and polls. 
# Read economic data. 
d_econ <- read_csv("fred_econ.csv") |> 
  filter(quarter == 2)
```

```
## Rows: 387 Columns: 14
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (14): year, quarter, GDP, GDP_growth_quarterly, RDPI, RDPI_growth_quarte...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
# Combine datasets and create vote lags. 
d_combined <- d_econ |> 
  left_join(d_poll_weeks, by = "year") |> 
  filter(year %in% c(unique(d_vote$year), 2024)) |> 
  group_by(party) |> 
  mutate(pv2p_lag1 = lag(pv2p, 1), 
         pv2p_lag2 = lag(pv2p, 2)) |> 
  ungroup() |> 
  mutate(gdp_growth_x_incumbent = GDP_growth_quarterly * incumbent, 
         rdpi_growth_quarterly = RDPI_growth_quarterly * incumbent,
         cpi_x_incumbent = CPI * incumbent,
         unemployment_x_incumbent = unemployment * incumbent,
         sp500_x_incumbent = sp500_close * incumbent) # Generate interaction effects.
```


```r
# Create fundamentals-only dataset and split into training and test sets. 
d_fund_inc <- d_combined |> 
  filter(incumbent) |> 
  select("year", "pv2p", "GDP", "GDP_growth_quarterly", "RDPI", "RDPI_growth_quarterly", "CPI", "unemployment", "sp500_close",
         "rdpi_growth_quarterly", "pv2p_lag1", "pv2p_lag2") 
x.train.fund <- d_fund_inc |> 
  filter(year <= 2020) |>
  select(-c(year, pv2p)) |> 
  slice(-1) |> 
  as.matrix()
y.train.fund <- d_fund_inc |> 
  filter(year <= 2020) |> 
  select(pv2p) |> 
  slice(-1) |> 
  as.matrix()
x.test.fund <- d_fund_inc |> 
  filter(year == 2024) |> 
  select(-c(year, pv2p)) |> 
  drop_na() |> 
  as.matrix()
```


```r
# Estimate elastic-net using fundamental variables only.
set.seed(02138)
enet.fund <- cv.glmnet(x = x.train.fund, y = y.train.fund, intercept = FALSE, alpha = 0.5)
```

```
## Warning: Option grouped=FALSE enforced in cv.glmnet, since < 3 observations per
## fold
```

```r
lambda.min.enet.fund <- enet.fund$lambda.min
```


```r
# Predict 2024 national pv2p share using elastic-net. 
(fund.pred <- predict(enet.fund, s = lambda.min.enet.fund, newx = x.test.fund))
```

```
##            s1
## [1,] 47.59299
```


```r
# Sequester data for combined model.
d_combo_inc <- d_combined |> 
  filter(incumbent) |> 
  select("year", "pv2p", "GDP", "GDP_growth_quarterly", "RDPI", "RDPI_growth_quarterly", "CPI", "unemployment", "sp500_close",
         "rdpi_growth_quarterly", "pv2p_lag1", "pv2p_lag2", all_of(paste0("poll_weeks_left_", 7:30))) 

x.train.combined <- d_combo_inc |> 
  filter(year <= 2020) |> 
  select(-c(year, pv2p)) |> 
  slice(-1) |> 
  as.matrix()
y.train.combined <- d_combo_inc |>
  filter(year <= 2020) |> 
  select(pv2p) |> 
  slice(-1) |> 
  as.matrix()
x.test.combined <- d_combo_inc |>
  filter(year == 2024) |> 
  select(-c(year, pv2p)) |> 
  drop_na() |> 
  as.matrix()
```


```r
# Estimate combined model.
set.seed(02138)
enet.combined <- cv.glmnet(x = x.train.combined, y = y.train.combined, intercept = FALSE, alpha = 0.5)
```

```
## Warning: Option grouped=FALSE enforced in cv.glmnet, since < 3 observations per
## fold
```

```r
lambda.min.enet.combined <- enet.combined$lambda.min
```


```r
# Predict 2024 national pv2p share using elastic-net.
(combo.pred <- predict(enet.combined, s = lambda.min.enet.combined, newx = x.test.combined))
```

```
##            s1
## [1,] 44.81875
```


```r
# Ensemble 1: Predict based on unweighted (or equally weighted) ensemble model between polls and fundamentals models. 
(unweighted.ensemble.pred <- (polls.pred + fund.pred)/2)
```

```
##            s1
## [1,] 48.15451
```


```r
# Ensemble 2: Weight based on polls mattering closer to November. (Nate Silver)
election_day_2024 <- "2024-11-05"
today <- "2024-09-18"
days_left <- as.numeric(as.Date(election_day_2024) - as.Date(today))

(poll_model_weight <- 1- (1/sqrt(days_left)))
```

```
## [1] 0.8556624
```

```r
(fund_model_weight <- 1/sqrt(days_left))
```

```
## [1] 0.1443376
```

```r
(ensemble.2.pred <- polls.pred * poll_model_weight + fund.pred * fund_model_weight)  
```

```
##            s1
## [1,] 48.55393
```


```r
# Ensemble 3. Weight based on fundamentals mattering closer to November. (Gelman & King, 1993)
(poll_model_weight <- 1/sqrt(days_left))
```

```
## [1] 0.1443376
```

```r
(fund_model_weight <- 1-(1/sqrt(days_left)))
```

```
## [1] 0.8556624
```

```r
(ensemble.3.pred <- polls.pred * poll_model_weight + fund.pred * fund_model_weight)
```

```
##            s1
## [1,] 47.75509
```
####----------------------------------------------------------#
#### Super learning at the state level for swing states.
####----------------------------------------------------------#

```r
# Get set of states where we have polling data for 2024 according to 538 poll averages.
states_2024 <- d_pollav_state$state[d_pollav_state$year == 2024] |> unique()
```


```r
# Predicting for Democratic incumbents.
# Simplifications and assumptions: 
  # Assuming Harris can be treated as incumbent for 2024 (could test either)
  # Getting weights from testing models on 2020 (could do different years)
  # Pooled models (could run state-specific models)
  # Using LOO-CV on 2020 (could do K-fold CV)
  # Using average poll support across all 30 weeks until election (could do weekly support, various imputation methods)
d_state_combo <- d_pollav_state |> 
  filter((state %in% states_2024)) |> 
  group_by(year, state, party) |>
  mutate(mean_pollav = mean(poll_support)) |>
  top_n(1, poll_date) |> 
  rename(latest_pollav = poll_support) |> 
  ungroup() |> 
  left_join(d_vote |> select(-pv, -pv2p), by = c("year", "party")) |> 
  filter(party == "DEM") |> 
  left_join(d_state_vote_wide, by = c("year", "state")) 
```


```r
# Model 1. Polling averages only. 
# Estimate model.
mod_1 <- lm(D_pv2p ~ latest_pollav + mean_pollav, 
            data = subset(d_state_combo, year < 2020))
```


```r
# Model 2. Lagged vote model. 
mod_2 <- lm(D_pv2p ~ D_pv2p_lag1 + D_pv2p_lag2, 
            data = subset(d_state_combo, year < 2020))
```


```r
# Model 3. Combined models. 
mod_3 <- lm(D_pv2p ~ incumbent + latest_pollav + mean_pollav + D_pv2p_lag1 + D_pv2p_lag2, 
            data = subset(d_state_combo, year < 2020))
```


```r
# Predictions from each model. 
pred_1 <- as.numeric(predict(mod_1, newdata = subset(d_state_combo, year == 2020)))
pred_2 <- as.numeric(predict(mod_2, newdata = subset(d_state_combo, year == 2020)))
pred_3 <- as.numeric(predict(mod_3, newdata = subset(d_state_combo, year == 2020)))
```


```r
# Get weights to build super learner. 
d_weight <- data.frame("truth" = d_state_combo$D_pv2p[d_state_combo$year == 2020],
                       "polls" = pred_1,
                       "lag_vote" = pred_2,
                       "combo" = pred_3)
```


```r
# Constrained optimization for ensemble mod weights. 
mod_ensemble <- lm(truth ~ polls + lag_vote + combo, 
                   data = d_weight)
```


```r
# Get weights and estimated weighted ensemble via constrained regression.
c <- 3 # number of models
predictions <- cbind(pred_1, pred_2, pred_3)
y.test <- d_weight$truth
w <- lm(y.test ~ predictions-1)
beta <- Variable(c)
objective <- Minimize(sum_squares(y.test - predictions %*% beta))
prob <- Problem(objective)
constraints(prob) <- list(beta >= 0, beta <= 1)
solution_prob <- solve(prob)
weights <- solution_prob$getValue(beta)
```


```r
# Predict using previous model output.
ensemble_pred <- cbind("state" = subset(d_state_combo, year == 2020)$state,
                       "pred" = round(as.numeric(t(weights) %*% t(predictions)), 3)) |> 
  as.data.frame()

ensemble_pred <- ensemble_pred |> 
  mutate(winner = ifelse(pred > 50, "D", "R"))

ensemble_pred
```

```
##             state   pred winner
## 1       Wisconsin 52.277      D
## 2        Virginia 54.681      D
## 3           Texas 49.352      R
## 4    Pennsylvania 50.596      D
## 5            Ohio 46.866      R
## 6  North Carolina 49.832      R
## 7        New York  61.19      D
## 8   New Hampshire 53.933      D
## 9          Nevada 50.815      D
## 10      Minnesota 51.821      D
## 11       Michigan 51.114      D
## 12        Georgia 50.206      D
## 13        Florida 50.004      D
## 14     California 61.701      D
## 15        Arizona 50.292      D
```
# Merge with electoral college dataset and make plots. 
# TODO: 

                             
                             
 Citations
 [1] - https://www.opensecrets.org/elections-overview/reelection-rates
 [2] - https://slcc.pressbooks.pub/attenuateddemocracy/chapter/chapter-55/ 
 [3] - https://www.opensecrets.org/political-action-committees-pacs/what-is-a-pac
                             
                             
                             
