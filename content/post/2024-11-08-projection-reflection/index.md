---
title: Projection Reflection
author: Victor Bowker
date: '2024-11-08'
slug: projection-reflection
categories: []
tags: []
---

# It Was the Economy, Stupid

Welcome back! The dust has settled, and President Trump has been re-elected. Nearly every precinct in the country went more to the right than in 2020. Isn't that interesting? In the following notes, I will remind you of my model, discuss what I think went wrong, and discuss how I would improve my projection in the future. Thanks again for reading!

# Recap of My Model

For my 2024 Presidential Election Forecast, I utilized polling data from September and October, as well as campaign event data and a variable on the incumbent status of the candidate. See below.






























```r
reg44 <- lm(D_pv2p ~ September_Results + October_Results + fun_campaign_events + incumbent_party, 
                data = model44)
```

The above prediction resulted in the a Harris projected win. As you likely know, Vice President Kamala Harris did not win this election. I will break down specific reasons for my miss below.









Here, you will see my prediction on a map of the US. If you were watching the Election Night broadcasts as closely as I was, you will know that only a few states on this map really decided the election.

First, for the states I forecasted correctly. In Georgia, I predicted Trump to win 50.24% of the vote share, while in fact he won 50.7%, according to AP. This was a pinnacle race and the blue hub of Atlanta simply did not pull through the way many expected.

Trump won Arizona with 52.2% of the vote, where I predicted he would seize 50.65%. This was a more anticipated outcome, but still played into Trump's win!

Additionally, in Nevada I forecasted Trump to win 50.14%, where he truly won 50.6%! As you see, in the states I predicted Trump winning, I was not *too* far off. The states that I erroneously gave to Harris, however, had a greater impact.

In Pennsylvania, I gave Harris a win, with 50.23% of the vote share, while in truth she only seized 48.6%. With Michigan and Wisconsin, Trump won both, taking off from my projection that had Harris taking both states.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-20-1.png" width="672" />

The above state map ended with a prediction that Trump would fall short with 268 Electoral Votes. In reality, the AP has called Trump with 312 Electoral Votes—a substantial difference, when single votes count very heavily!

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-21-1.png" width="672" />

# Why Was I Wrong?

After every election, incorrect electoral projectors must ask themselves one question: what happened?

The best answer is that I ignored the economy. My projection was only state-based, and in turn, I did not leverage any economic data. If I had included data on GDP growth, RDPI, or inflation, I expect my projection would have been a lot more favored toward Trump. We see time and time again that the economy is an incredibly important factor. While social issues were the forefront of Harris' campaign, Trump's solid economy first messaging seemingly prevailed. When it comes time to vote, I hypothesize that Americans truly chose their wallet over their heart.

Additionally, it appears that I had some coding errors in my merging of polling data. I am looking into the problem, but admittedly staring at .csv files isn't my *favorite* thing to do! Due to this error, my polling data had less influence over the projection.

The best way to test this hypothesis would be to find state based economic data, clean and organize it, and then weigh it heavily in a projection model. I anticipate that if provided with data on RDPI or inflation, my prediction would be a lot more red than it currently stands

On top of adding economic data, I would remove the campaign events variable. We see that Harris *greatly* outperformed Trump in spending, holding more events with better attendance, but she still lost. I did not include data on spending, but I believe it is fair to assume that more money means more events! The ground game is *generally* a valuable asset to campaigns, but perhaps it did not pull through this time!
