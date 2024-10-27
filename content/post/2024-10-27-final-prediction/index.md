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

Can you believe it? This is my final post before the 2024 Presidential General Election, where either Former President Donald Trump, or Vice President Kamala Harris, will be elected the next President of the United States. I think

``` r
d_campaign_events <- read_csv("campaign_events_geocoded.csv")
```

    ## Rows: 902 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (4): state, city, candidate, Event.Type
    ## dbl  (3): year, latitude, longitude
    ## date (1): date
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
d_campaign_events$party[d_campaign_events$candidate %in% c("Trump / Pence", "Trump", "Pence", "Trump/Pence", "Vance")] <- "REP"
```

    ## Warning: Unknown or uninitialised column: `party`.

``` r
d_campaign_events$party[d_campaign_events$candidate %in% c("Biden / Harris", "Biden", "Harris", "Biden/Harris", "Walz", "Kaine", "Clinton", "Clinton / Kaine")] <- "DEM"

d_campaign_events
```

    ## # A tibble: 902 × 9
    ##    date       state city     candidate Event.Type  year latitude longitude party
    ##    <date>     <chr> <chr>    <chr>     <chr>      <dbl>    <dbl>     <dbl> <chr>
    ##  1 2016-07-25 VA    Roanoke  Trump / … Town Hall   2016     37.3     -79.9 REP  
    ##  2 2016-07-25 NC    Winston… Trump / … Rally/Spe…  2016     36.1     -80.2 REP  
    ##  3 2016-07-27 FL    Doral    Trump     Speech/Pr…  2016     25.8     -80.4 REP  
    ##  4 2016-07-27 PA    Scranton Trump / … Rally/Spe…  2016     41.4     -75.7 REP  
    ##  5 2016-07-27 WI    Waukesha Pence     Rally/Spe…  2016     43.0     -88.2 REP  
    ##  6 2016-07-27 OH    Toledo   Trump     Rally/Spe…  2016     41.7     -83.5 REP  
    ##  7 2016-07-28 MI    Grand R… Pence     Rally/Spe…  2016     43.0     -85.7 REP  
    ##  8 2016-07-28 MI    Novi     Pence     Rally/Spe…  2016     42.5     -83.5 REP  
    ##  9 2016-07-28 IA    Cedar R… Trump     Rally/Spe…  2016     42.0     -91.7 REP  
    ## 10 2016-07-28 IA    Davenpo… Trump     Rally/Spe…  2016     41.5     -90.6 REP  
    ## # ℹ 892 more rows

<div class="datatables html-widget html-fill-item" id="htmlwidget-1" style="width:100%;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"filter":"none","vertical":false,"caption":"<caption>Updated Regression Results<\/caption>","data":[["1","2","3","4"],["(Intercept)","September_Results","October_Results","fun_campaign_events"],[8.34395344745049,0.611420704539272,0.2241231547885874,-41.8521345306346],[6.523508463530661,0.113605110172749,0.1365874817597192,14.82973552224305],[1.27905918940658,5.381982409149902,1.64087624942715,-2.822176731868265],[0.2036431587206929,4.384318365979549e-07,0.103759502500305,0.005687984014582276]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>term<\/th>\n      <th>estimate<\/th>\n      <th>std.error<\/th>\n      <th>statistic<\/th>\n      <th>p.value<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"pageLength":4,"columnDefs":[{"className":"dt-right","targets":[2,3,4,5]},{"orderable":false,"targets":0},{"name":" ","targets":0},{"name":"term","targets":1},{"name":"estimate","targets":2},{"name":"std.error","targets":3},{"name":"statistic","targets":4},{"name":"p.value","targets":5}],"order":[],"autoWidth":false,"orderClasses":false,"lengthMenu":[4,10,25,50,100]},"selection":{"mode":"multiple","selected":null,"target":"row","selectable":null}},"evals":[],"jsHooks":[]}</script>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-22-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-23-1.png" width="672" />
