---
title: Blog Post 3
author: Package Build
date: '2024-09-18'
slug: blog-post-3
categories: []
tags: []
---




<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />



```
## 
## Call:
## lm(formula = pv2p ~ nov_poll, data = subset(d_poll_nov, party == 
##     "DEM"))
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -4.0155 -2.4353 -0.3752  1.4026  5.8014 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  14.2936     7.1693   1.994 0.069416 .  
## nov_poll      0.7856     0.1608   4.885 0.000376 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.968 on 12 degrees of freedom
## Multiple R-squared:  0.6654,	Adjusted R-squared:  0.6375 
## F-statistic: 23.86 on 1 and 12 DF,  p-value: 0.0003756
```

```
## 
## Call:
## lm(formula = pv2p ~ nov_poll, data = d_poll_nov)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -4.6190 -1.6523 -0.5808  1.3629  6.0220 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 17.92577    4.15543   4.314 0.000205 ***
## nov_poll     0.70787    0.09099   7.780 2.97e-08 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.75 on 26 degrees of freedom
## Multiple R-squared:  0.6995,	Adjusted R-squared:  0.6879 
## F-statistic: 60.52 on 1 and 26 DF,  p-value: 2.974e-08
```



```
## 
## Call:
## lm(formula = paste0("pv2p ~ ", paste0("poll_weeks_left_", 0:30, 
##     collapse = " + ")), data = d_poll_weeks_train)
## 
## Residuals:
## ALL 28 residuals are 0: no residual degrees of freedom!
## 
## Coefficients: (4 not defined because of singularities)
##                    Estimate Std. Error t value Pr(>|t|)
## (Intercept)        28.25534        NaN     NaN      NaN
## poll_weeks_left_0   3.24113        NaN     NaN      NaN
## poll_weeks_left_1   0.02516        NaN     NaN      NaN
## poll_weeks_left_2  -8.87360        NaN     NaN      NaN
## poll_weeks_left_3   7.91455        NaN     NaN      NaN
## poll_weeks_left_4   0.74573        NaN     NaN      NaN
## poll_weeks_left_5   1.41567        NaN     NaN      NaN
## poll_weeks_left_6  -4.58444        NaN     NaN      NaN
## poll_weeks_left_7   4.63361        NaN     NaN      NaN
## poll_weeks_left_8  -0.95121        NaN     NaN      NaN
## poll_weeks_left_9  -1.55307        NaN     NaN      NaN
## poll_weeks_left_10 -1.38062        NaN     NaN      NaN
## poll_weeks_left_11  1.74881        NaN     NaN      NaN
## poll_weeks_left_12 -1.28871        NaN     NaN      NaN
## poll_weeks_left_13 -0.08482        NaN     NaN      NaN
## poll_weeks_left_14  0.87498        NaN     NaN      NaN
## poll_weeks_left_15 -0.16310        NaN     NaN      NaN
## poll_weeks_left_16 -0.34501        NaN     NaN      NaN
## poll_weeks_left_17 -0.38689        NaN     NaN      NaN
## poll_weeks_left_18 -0.06281        NaN     NaN      NaN
## poll_weeks_left_19 -0.17204        NaN     NaN      NaN
## poll_weeks_left_20  1.52230        NaN     NaN      NaN
## poll_weeks_left_21 -0.72487        NaN     NaN      NaN
## poll_weeks_left_22 -2.76531        NaN     NaN      NaN
## poll_weeks_left_23  4.90361        NaN     NaN      NaN
## poll_weeks_left_24 -2.04431        NaN     NaN      NaN
## poll_weeks_left_25 -0.76078        NaN     NaN      NaN
## poll_weeks_left_26 -0.47860        NaN     NaN      NaN
## poll_weeks_left_27       NA         NA      NA       NA
## poll_weeks_left_28       NA         NA      NA       NA
## poll_weeks_left_29       NA         NA      NA       NA
## poll_weeks_left_30       NA         NA      NA       NA
## 
## Residual standard error: NaN on 0 degrees of freedom
## Multiple R-squared:      1,	Adjusted R-squared:    NaN 
## F-statistic:   NaN on 27 and 0 DF,  p-value: NA
```


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-17-1.png" width="672" />

```
## 32 x 1 sparse Matrix of class "dgCMatrix"
##                              s1
## (Intercept)        29.951147799
## poll_weeks_left_0   0.032163983
## poll_weeks_left_1   0.025440084
## poll_weeks_left_2   0.024404320
## poll_weeks_left_3   0.024688870
## poll_weeks_left_4   0.024695646
## poll_weeks_left_5   0.024725772
## poll_weeks_left_6   0.024080438
## poll_weeks_left_7   0.023636908
## poll_weeks_left_8   0.024487501
## poll_weeks_left_9   0.026498950
## poll_weeks_left_10  0.025642838
## poll_weeks_left_11  0.021361476
## poll_weeks_left_12  0.017386999
## poll_weeks_left_13  0.013378030
## poll_weeks_left_14  0.010078675
## poll_weeks_left_15  0.007248494
## poll_weeks_left_16  0.012943440
## poll_weeks_left_17  0.012879654
## poll_weeks_left_18  0.011157452
## poll_weeks_left_19  0.008302783
## poll_weeks_left_20  0.004012987
## poll_weeks_left_21  0.003350434
## poll_weeks_left_22  0.004458406
## poll_weeks_left_23  0.001019583
## poll_weeks_left_24 -0.002711193
## poll_weeks_left_25 -0.002447895
## poll_weeks_left_26  0.001121142
## poll_weeks_left_27  0.005975853
## poll_weeks_left_28  0.011623984
## poll_weeks_left_29  0.013833925
## poll_weeks_left_30  0.018964139
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-20-1.png" width="672" />

```
## 32 x 1 sparse Matrix of class "dgCMatrix"
##                             s1
## (Intercept)        24.57897724
## poll_weeks_left_0   0.50149421
## poll_weeks_left_1   .         
## poll_weeks_left_2   .         
## poll_weeks_left_3   .         
## poll_weeks_left_4   .         
## poll_weeks_left_5   0.08461518
## poll_weeks_left_6   .         
## poll_weeks_left_7   .         
## poll_weeks_left_8   .         
## poll_weeks_left_9   0.17064525
## poll_weeks_left_10  .         
## poll_weeks_left_11  .         
## poll_weeks_left_12  .         
## poll_weeks_left_13  .         
## poll_weeks_left_14  .         
## poll_weeks_left_15  0.01147512
## poll_weeks_left_16  .         
## poll_weeks_left_17  .         
## poll_weeks_left_18  0.23694416
## poll_weeks_left_19  .         
## poll_weeks_left_20  .         
## poll_weeks_left_21  .         
## poll_weeks_left_22  .         
## poll_weeks_left_23  .         
## poll_weeks_left_24  .         
## poll_weeks_left_25 -0.55693209
## poll_weeks_left_26  .         
## poll_weeks_left_27  .         
## poll_weeks_left_28  .         
## poll_weeks_left_29  .         
## poll_weeks_left_30  0.11120476
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-23-1.png" width="672" />



```
## [1] 9.575001
```

```
## [1] 4.642786
```

```
## [1] 3.533155
```
<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-27-1.png" width="672" />

```
## [1]  7 36
```


```
##            s1
## [1,] 51.79268
## [2,] 50.65879
```





```
##            s1
## [1,] 51.23438
## [2,] 47.63135
```






```
##           s1
## [1,] 50.4831
## [2,] 47.9374
```

```
##            s1
## [1,] 51.51353
## [2,] 49.14507
```

```
## [1] 0.8556624
```

```
## [1] 0.1443376
```

```
##            s1
## [1,] 51.71210
## [2,] 50.22182
```

```
## [1] 0.1443376
```

```
## [1] 0.8556624
```

```
##            s1
## [1,] 51.31497
## [2,] 48.06832
```

**Extension Comparing Silver and Morris**

  In 538’s polling, they have created a forecast model that ties many factors together for what they hope is the most accurate prediction of the election. First, they make some tweaks to the data to account for a few key events. In the days of and soon after a national convention, 538 makes downward adjustments to make up for the likely uptick in support. They made it clear that these recalibrations only occur if there was a substantial change in support, so candidates with little change are not impacted. 538 justifies this because both Trump and Clinton had their highest daily polling averages in the week during and after their respective national conventions. 
	Additionally, 538 is not afraid to make calculated assumptions about certain regions of America. Their forecasting model will detect an uptick in support for Biden in Maine, and begin to raise projections for him in Vermont New Hampshire, or other like-minded New England states. 538 has set up a map of 10 regions across the US that represent geographically, economically, and socially similar groups of states. My favorite of those groups is Tex-ish, which includes the great states of Texas, Louisiana, and Oklahoma. 
	Next, 538 polls on buckets of factors, like economic indicators including jobs, spending, personal income, and manufacturing. The motivation for these distinctions comes from the issue of only tracking GDP: it is too slow. The model has been trained on historical measures of this data, some of which go back nearly 100 years. Another bucket includes info on political factors, like office incumbency status or party incumbency status. By combining fundamental measures of economic growth and public opinion with this new, advanced forecast model, 538 is able to present an incredibly accurate prediction of the next election!

  Nate Silver, a former 538 pollster, has a similar forecast model, with a few key differences. The last presidential election under Silver’s purview was 2020, meaning there were extensive COVID adjustments that have to now be subtracted from the equation. COVID is simply not a factor of any grand scale in this election.
	Silver also has seen a change in who turns out for elections, leading to a change in the forecast model. With evidence from special elections and primaries, it is clear that Republicans no longer turn out in larger numbers than Democrats. Adjustments to scale who answer polls now have to shift from turning down Republican responses to Democratic ones. He is also planning to fully phase out this turnout measurement before Election Day. 
	Another important factor that was phased out this term is the Cost of Voting Index. This measurement assumed that as states loosened laws surrounding voting, like same-day registration, Democrats would benefit. Alternatively, if a state was to shorten polling place hours, or restrict registration, Republicans would be likely to benefit. Silver has deemed this an ineffective metric and has removed it from his forecast. 
	Next, Silver had to consider the presence of a third-party named candidate. In this race, Robert Kennedy Jr. was running as an Independent candidate before dropping out and supporting Former President Trump. 2020 had no impactful third-party candidate, but 2016 did have Gary Johnson, for whom the forecast was originally based. Silver found that third-party candidates usually started with decent polling, before slowly fading as Election Day loomed. Additionally, polls utilized varied wording for a third-party candidate, further confusing the ability to accurately measure popular opinion on less mainstream candidates. 
	Finally, Silver had to consider this race being a presidential rematch, where Biden took on Trump a second time. This has since changed now that the Democratic candidate has switched from President Joe Biden to Vice President Kamala Harris. Now, the reliability of pre-dropout data is difficult to trust or demonstrate change. 

Overall, I believe that 538’s approach is stronger, exactly because it glazes over some of Silver’s nuance. When you hyper-fixate on these small characteristics of an election, it is very possible that the forecast can be more accurate–but we are also fully aware that a very small amount of voters in key swing districts in key swing states will decide this election. 

End of Story!

