---
title: Projection Reflection
author: Victor Bowker
date: '2024-11-08'
slug: projection-reflection
categories: []
tags: []
---

# Well, I was wrong

More thoughts to follow

# Recap of My Model

For my 2024 Presidential Election Forecast, I utilized polling data from September and October, as well as campaign event data and a variable on the incumbent status of the candidate. See below.






























```r
reg44 <- lm(D_pv2p ~ September_Results + October_Results + fun_campaign_events + incumbent_party, 
                data = model44)
```

The above prediction resulted in the a Harris projected win. As you likely know, Vice President Kamala Harris did not win this election. I will break down specific reasons for my miss below.









<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-20-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-21-1.png" width="672" />
