---
title: Final Prediction
author: Victor Bowker
date: '2024-10-27'
slug: final-prediction
categories: []
tags: []
---

<link href="{{< blogdown/postref >}}index_files/htmltools-fill/fill.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/datatables-css/datatables-crosstalk.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/datatables-binding/datatables.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery-3.6.0.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/dt-core/css/jquery.dataTables.min.css" rel="stylesheet" />
<link href="{{< blogdown/postref >}}index_files/dt-core/css/jquery.dataTables.extra.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/dt-core/js/jquery.dataTables.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>

# Disregard - Incomplete

1)  model formula (or procedure for obtaining prediction),
2)  model description and justification,
3)  coefficients (if using singular regression) and/or weights (if using ensemble of different models) and/or feature importance (if using machine learning)
4)  interpretation of coefficients, feature importance, and/or justification of weights,
5)  model validation (recommended to include both in-sample and out-of-sample performance unless it is impossible due to the characteristics of model and related data availability),
6)  uncertainty around prediction (e.g. predictive interval)
7)  graphic(s) showing your prediction

# Welcome, Again

Can you believe it? This is my final post before the 2024 Presidential General Election, where either Former President Donald Trump, or Vice President Kamala Harris, will be elected the next President of the United States.

Below, you will find a culmination of nearly a semester of learning and projecting. I want to extend a special shout out to the teaching team of Gov 1347: Election Analytics, including Professor Ryan Enos, Teaching Fellow Matthew Dardet, and Course Assistants Yusuf Mian and Ethan Jasny! Over the past two months, we have met weekly to discuss each aspect of a political campaign, through guest speakers and in class discussions. I have enjoyed this class incredibly, and I am so excited to see how my projection matches up with the professional ones! Last person I will shout out before getting to the projection is my dear friend Kaitlyn Vu, a fellow Gov concentrating sophomore in Gov 1347 - she is great, and you can check out here projection here: <https://kaitvu.github.io/election-blog/>

# The Model I Used

``` r
reg44 <- lm(D_pv2p ~ September_Results + October_Results + fun_campaign_events, 
                data = model44)
```

This model is a multiple linear regression aimed at predicting the Democratic popular vote share (`D_pv2p)` using polling data and campaign events. September and October Polling results come from data published on *FiveThirtyEight* which was organized by CAs Ethan Jasny and Yusuf Mian. Campaign event data was tidied by our lovely 1347 CAs as well!

# Analysis of Regression

This regression was run with four (4) variables, including the intercept, September Polling Results, October Polling Results, and a variable on the location and timing of campaign events.

First, you will see that the intercept’s p-value is .203, which is above the 0.05 threshold, meaning it is not statistically significant at the expected 5% value.

Alternatively, September Results yield more encouraging results, showing that with a p-value of 4.38e-7, the effects of September polling is incredibly significant in the final projection of the dependent variable! You will see that with an estimate of 0.61, each point increase in September polling reflects the Democratic vote share to increase by 0.61 points!

Next up, October Results are not as impactful—but I have kept them in. In class, we discussed heavily how often voters are swayed in the weeks leading up to an election: they generally don’t consider events of 1 or 2 years ago, when they can think about what happened this week. With a p-value of 0.103, the regression model finds the variable to be not statistically significant.

Finally, it is time to discuss the campaign events. You will notice something particularly strange about the estimate in this line. With a low p-value, the variable is seen to be statistically significant. With the estimate, it appears that for every additional campaign event held, the Democrats party vote share will decrease by nearly 42 units. We learned during the ground game discussion in class that the impact of campaign offices and events can be great-but my model does not agree. We know that funding for events has skyrocketed, but perhaps my model is correct in knowing that these events are merely a spectacle—or as we recently saw, a chance to assassinate the Former President.

<div class="datatables html-widget html-fill-item" id="htmlwidget-1" style="width:100%;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"filter":"none","vertical":false,"caption":"<caption>Updated Regression Results<\/caption>","data":[["1","2","3","4"],["(Intercept)","September_Results","October_Results","fun_campaign_events"],[8.34395344745049,0.611420704539272,0.2241231547885874,-41.8521345306346],[6.523508463530661,0.113605110172749,0.1365874817597192,14.82973552224305],[1.27905918940658,5.381982409149902,1.64087624942715,-2.822176731868265],[0.2036431587206929,4.384318365979549e-07,0.103759502500305,0.005687984014582276]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>term<\/th>\n      <th>estimate<\/th>\n      <th>std.error<\/th>\n      <th>statistic<\/th>\n      <th>p.value<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"pageLength":4,"columnDefs":[{"className":"dt-right","targets":[2,3,4,5]},{"orderable":false,"targets":0},{"name":" ","targets":0},{"name":"term","targets":1},{"name":"estimate","targets":2},{"name":"std.error","targets":3},{"name":"statistic","targets":4},{"name":"p.value","targets":5}],"order":[],"autoWidth":false,"orderClasses":false,"lengthMenu":[4,10,25,50,100]},"selection":{"mode":"multiple","selected":null,"target":"row","selectable":null}},"evals":[],"jsHooks":[]}</script>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-21-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-22-1.png" width="672" />
