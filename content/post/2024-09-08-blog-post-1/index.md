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

One of the more critical aspects of forecasting is understanding the past. Data can be an incredible tool in understanding past elections, will will allow us to predict the next ones. Below, you will see the two party national vote distribution for the past ~70 years, from 1948 to 2020. You should note that elections are closer now than at most times in our recent history. This can make projections more difficult, as votes are less unanimous!















<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="672" />














Next, see how this same presidential vote share can be broken down by each, by year. Comparing this with the historical winners of each respective election, you can better understand how states have historically voted, and how impactful their vote was. It is no secret that some states, like Wyoming, have so few votes that generally their electoral votes will not sway an election. Never the less, viewing by state vote share allows you to understand what public opinion can do to individual state's voting tendencies.

```
## Warning in left_join(filter(d_pvstate_wide, year >= 1980), states_map, by = "region"): Detected an unexpected many-to-many relationship between `x` and `y`.
## ℹ Row 1 of `x` matches multiple rows in `y`.
## ℹ Row 1 of `y` matches multiple rows in `x`.
## ℹ If a many-to-many relationship is expected, set `relationship =
##   "many-to-many"` to silence this warning.
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-14-1.png" width="672" />









Now, on to our current prediction, for the 2024 National Election. Per the tibble below, Kamala Harris and the Democrats will narrowly take the lead over Donald Trump. Now, what do we see? First, there are the expected Democrat strongholds in the Northeast and West Coast. In Wisconsin, my forecast agrees with the newest CNN poll that VP Harris will narrowly take the lead.* Interestingly, CNN is more confident in their projection that President Trump can clinch Arizona, where my data is not as certain. This race will be _close_, and I am excited to continue updating projections as we get closer to Election Day!

```
## Warning: Removed 12 rows containing missing values (`geom_text()`).
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-19-1.png" width="672" />

CNN Source: https://www.cnn.com/2024/09/04/politics/cnn-polls-battleground-states/index.html
Some code utilized from TF Matthew Dardet as well as online sources included StackOverflow and ChatGPT 4






```
## # A tibble: 2 × 2
##   winner electoral_votes
##   <chr>            <dbl>
## 1 D                  276
## 2 R                  262
```
