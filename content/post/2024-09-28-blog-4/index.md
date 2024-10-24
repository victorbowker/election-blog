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

That would simply be too easy--and ignoring too much information. We have seen many times where candidates lost as incumbents, like George H. W. Bush or Donald Trump. Additionally, there are many factors still at play that would be neglected if we simply look at past results. One example, which I looked into in past weeks, is the economy, where Goldman Sachs Political Economists have found that incumbents lose at higher rates during recessions than times of economic prosperity.[4]





**Analysis**

Lets talk about the infamous _pork barrel_. What an interesting phrase...with an even more interesting meaning. The general idea is politicians will add funding for seemingly random projects into a larger budget to benefit their constituents. This practice is very common because all politicians want to make their voters happy-or at least they want to win re-election. 

Now, in the graph below, you will see how states receive funding depending on the nature of the election's status. By status I mean whether the race was contentious or if there was an election that year. You will see below that swing states during election years receive the most federal grant spending with core election and non-election states receive the least, by the amount of nearly $50 million. 

Now, consider if incumbency matters...























<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-12-1.png" width="672" />

To further illustrate investigate importance, see below. This demonstrates how many post-war elections yielded a winner who served in the administration of the former president. In this case, only 27% of the winners were in the previous admin. 


```
## prev_admin
## FALSE  TRUE 
## 72.22 27.78
```





Below, you will see some analysis using the pork state model. With the data set used above, we see that a p-value of .92, the state's competitive status does not extensively impact the incumbent party's vote share. Additionally, we see that a change in grant money is not incredibly relevant to incumbent party's vote share.

So, what does this mean? Does it seem that porking does not work? It seems as though candidates work hard to provide funding to swing states, but with no impact.


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



















































































**Prediction**

Now, for 2024. In the same fashion as last week, it is time to predict the next President of the United States! Below, you will see a relevant state analysis of the next election. This is combining a few models, including the pork model we already discussed, as well as a model based on lagged vote, which considers results of past elections to project the next one!




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
      
**Trump vs. Harris Incumbency**

   In my quasi-educated position, it feels as though Former President Trump feels a greater incumbency advantage than Vice President Harris. Trump had some hefty [5] goals, and he accomplished _some_ of them. When called upon for things he did not accomplish, like building a border wall-and making Mexico pay for it-he blamed Congress, or Obama, or someone else. His voter base generally believed this, meaning his track record was only positive-in the minds of those who would vote for him.
   Vice President Harris, on the other hand, has been _less_ celebrated. Vice Presidents are typically blamed for failing at goals, but what goals do they really have? Often times, they are a failed presidential candidate that the nominee chooses to shape out a ticket. Pence is an example, Harris is another. It appears that VP Harris was blamed for a lot of things, especially things that perhaps VP Pence was not blamed for. Either way, she is far from a celebrated Vice President in the public opinion. She has the support of President Biden, but that is the only reason most people are supporting her, or because she is simply not Former President Donald Trump. 

                           
 Citations
 [1] - https://www.opensecrets.org/elections-overview/reelection-rates
 [2] - https://slcc.pressbooks.pub/attenuateddemocracy/chapter/chapter-55/ 
 [3] - https://www.opensecrets.org/political-action-committees-pacs/what-is-a-pac
 [4] - https://www.goldmansachs.com/insights/articles/us-president-incumbents-tend-to-win-elections-except-during-recessions   [5] - https://www.npr.org/2016/11/09/501451368/here-is-what-donald-trump-wants-to-do-in-his-first-100-days                     
                             
                             
