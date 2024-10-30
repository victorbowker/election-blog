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

# Welcome, Again

Can you believe it? This is my final post before the 2024 Presidential General Election, where either Former President Donald Trump, or Vice President Kamala Harris, will be elected the next President of the United States.

Below, you will find a culmination of nearly a semester of learning and projecting. I want to extend a special shout out to the teaching team of Gov 1347: Election Analytics, including Professor Ryan Enos, Teaching Fellow Matthew Dardet, and Course Assistants Yusuf Mian and Ethan Jasny! Over the past two months, we have met weekly to discuss each aspect of a political campaign, through guest speakers and in class discussions. I have enjoyed this class incredibly, and I am so excited to see how my projection matches up with the professional ones! Last person I will shout out before getting to the projection is my dear friend Kaitlyn Vu, a fellow Gov concentrating sophomore in Gov 1347 - she is great, and you can check out here projection here: <https://kaitvu.github.io/election-blog/>

# The Model I Used

``` r
reg44 <- lm(D_pv2p ~ September_Results + October_Results + fun_campaign_events + incumbent_party, 
                data = model44)
```

This model is a multiple linear regression aimed at predicting the Democratic popular vote share (`D_pv2p)` using polling data, campaign events, and the status of whether the party is an incumbent or challenger. September and October Polling results come from data published on *FiveThirtyEight* which was organized by CAs Ethan Jasny and Yusuf Mian. Campaign event data was tidied by our lovely 1347 CAs as well! Incumbent party data is compiled from history!

# Analysis of Regression

This regression was run with five (5) variables, including the intercept, September Polling Results, October Polling Results, whether the Democrats are the incumbent, and a variable on the location and timing of campaign events.

First, you will see that the intercept’s p-value is .62, which is above the 0.05 threshold, meaning it is not statistically significant at the expected 5% value.

Alternatively, September Results yield more encouraging results, showing that with a p-value of 3.16×10^−7, the effects of September polling is incredibly significant in the final projection of the dependent variable! You will see that with an estimate of 0.62, each point increase in September polling reflects the Democratic vote share to increase by 0.62 points!

Next up, October Results are not as impactful—but I have kept them in. In class, we discussed heavily how often voters are swayed in the weeks leading up to an election: they generally don’t consider events of 1 or 2 years ago, when they can think about what happened this week. With a p-value of 0.055, the regression model finds the variable to be marginally statistically significant. This means that while influential, the results of October Results are less informative than September - *interesting*!

Finally, it is time to discuss the campaign events. You will notice something particularly strange about the estimate in this line. With a low p-value, the variable is seen to be statistically significant. With the estimate, it appears that for every additional campaign event held, the Democrats party vote share will decrease by nearly 43 units. We learned during the ground game discussion in class that the impact of campaign offices and events can be great-but my model does not agree. We know that funding for events has skyrocketed, but perhaps my model is correct in knowing that these events are merely a spectacle—or as we recently saw, a chance to assassinate the Former President. I will be interested to see this outcome specifically, considering Former President Trump’s recent rally at Madison Square Garden, where a comedian shared some disrespectful jokes towards key demographics in Trumps reelection strategy.

<div class="datatables html-widget html-fill-item" id="htmlwidget-1" style="width:100%;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"filter":"none","vertical":false,"caption":"<caption>Updated Regression Results<\/caption>","data":[["1","2","3","4","5"],["(Intercept)","September_Results","October_Results","fun_campaign_events","incumbent_party"],[3.702068722508358,0.6206253184117408,0.2794855181164667,-43.35448927481564,3.553968687600939],[7.612760229679788,0.1136702467941809,0.1442261654962777,14.85800527400274,3.01922254604688],[0.4862978224475193,5.459874821381249,1.937828112913949,-2.917921246849576,1.177113854112613],[0.6277599033318632,3.162563923716879e-07,0.05530462794080629,0.004303025620167464,0.2417864445319952]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>term<\/th>\n      <th>estimate<\/th>\n      <th>std.error<\/th>\n      <th>statistic<\/th>\n      <th>p.value<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"pageLength":5,"columnDefs":[{"className":"dt-right","targets":[2,3,4,5]},{"orderable":false,"targets":0},{"name":" ","targets":0},{"name":"term","targets":1},{"name":"estimate","targets":2},{"name":"std.error","targets":3},{"name":"statistic","targets":4},{"name":"p.value","targets":5}],"order":[],"autoWidth":false,"orderClasses":false,"lengthMenu":[5,10,25,50,100]},"selection":{"mode":"multiple","selected":null,"target":"row","selectable":null}},"evals":[],"jsHooks":[]}</script>

# 2024 Election Projection

On the map below, you will see my final projection for the 2024 Presidential Election. As you will see, this has taken a turn from my past projections, where Harris now has an incredibly narrow lead. This has changed now that I have added in campaign events, as well as the incumbent advantage.

Barely, Harris wins this projection. Specifically, I have her seizing her typical blue states, as well as Wisconsin, Michigan, Pennsylvania. Trump takes Nevada, North Carolina, Arizona, and Georgia as well as his typical red states.

Take a look for yourself below!

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-21-1.png" width="672" />

# Electoral College Roundup

Below you will see a bar chart with my final projection for the 2024 Presidential Election. The green dashed line shows the threshold of 270 electoral votes — the amount needed to win the White House. Clearly, this election is *incredibly close*, at least according to my projection. Here, you will see that Harris takes the lead by only two electoral votes, winning 270 to 268.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-22-1.png" width="672" />

# Is This A Strong Formula?

Not really. I worked quite hard to investigate reasons for this disappointing R<sup>2</sup> , mostly to no avail. Below you will see results for an in-sample validation. The R<sup>2</sup> is 0.33, meaning it only accounts for 33% of outcomes in the Democratic two party vote share. That means this is not a highly consistent model, but in elections that are increasingly difficult to project, it happens sometimes! Either way, I know others used the exact same variables and had R<sup>2</sup> in the 0.8 region, but alas.

    ## 
    ## Call:
    ## lm(formula = D_pv2p ~ September_Results + October_Results + fun_campaign_events + 
    ##     incumbent_party, data = model44)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -55.873  -0.974   2.349   5.946  39.833 
    ## 
    ## Coefficients:
    ##                     Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)           3.7021     7.6128   0.486   0.6278    
    ## September_Results     0.6206     0.1137   5.460 3.16e-07 ***
    ## October_Results       0.2795     0.1442   1.938   0.0553 .  
    ## fun_campaign_events -43.3545    14.8580  -2.918   0.0043 ** 
    ## incumbent_party       3.5540     3.0192   1.177   0.2418    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 14.72 on 106 degrees of freedom
    ## Multiple R-squared:  0.3302,	Adjusted R-squared:  0.305 
    ## F-statistic: 13.07 on 4 and 106 DF,  p-value: 1.099e-08
