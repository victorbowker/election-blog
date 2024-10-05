---
title: Blog Post 5
author: Package Build
date: '2024-10-05'
slug: blog-post-5
categories: []
tags: []
---
#' @title GOV 1347: Week 5 (Demographics) Laboratory Session
#' @author
#' @date October 2, 2024

####----------------------------------------------------------#
#### Preamble
####----------------------------------------------------------#


## set working directory here
# setwd("~")






####----------------------------------------------------------#
#### Replication of Kim & Zilinsky (2023).
####----------------------------------------------------------#






**Demographics**

This week is _all about_ demographics, so lets talk about it!

When pollsters review data to make predictions, they have _a lot_ of factors to consider. I have covered some of these in prior posts, including economic factors, public opinion polls, and historical trends. Today, I will explore trends that are impacted--or are not--by demographics. The primary demographics included in today's data are race, gender, education level, income, religion, and a few others!

For the first regression of the way (woot woot we love regressions) take a look down below. This regression tells us which demographic factors have been historically most accurate, and which demonstrated less accurate results.

Interestingly, this form shows that age is not statistically significant in which party a candidate votes for. I say this is interesting because the Harvard Kennedy School Institute of Politics Spring 2024 Poll demonstrated that likely young voters were much more likely to vote for the Democrat (Biden) compared to the Republican (Trump). For voters under 30, Biden had the lead of 8 percentage points, which seemingly demonstrates something different than this-- _interesting_![1]

Additionally, I see that gender and race are in fact quite demonstrative of voting patterns, with negative coefficients of -0.429 and -0.548 respectively. According to the Pew Research Center, data shows that black voters turnout less than white voters, but overwhelmingly vote for Democrats, with roughly 93% of black voters voting for Democrats in the 2022 midterm elections!







```
## 
## Logistic Regression Results
## =============================================
##                       Dependent variable:    
##                   ---------------------------
##                            pres_vote         
## ---------------------------------------------
## age                          0.001           
##                             (0.003)          
##                                              
## gender                     -0.429***         
##                             (0.093)          
##                                              
## race                       -0.548***         
##                             (0.061)          
##                                              
## educ                       -0.340***         
##                             (0.061)          
##                                              
## income                       0.049           
##                             (0.047)          
##                                              
## religion                   -0.215***         
##                             (0.042)          
##                                              
## attend_church              -0.211***         
##                             (0.033)          
##                                              
## southern                   -0.410***         
##                             (0.105)          
##                                              
## region                                       
##                                              
##                                              
## work_status                 0.096**          
##                             (0.046)          
##                                              
## homeowner                  -0.177**          
##                             (0.082)          
##                                              
## married                    -0.072***         
##                             (0.028)          
##                                              
## Constant                   4.358***          
##                             (0.437)          
##                                              
## ---------------------------------------------
## Observations                 2,088           
## Log Likelihood            -1,282.131         
## Akaike Inf. Crit.          2,588.262         
## =============================================
## Note:             *p<0.1; **p<0.05; ***p<0.01
```






# Can also write loop to compute values by year and replicate plots from Kim & Zilinsky's (2023) paper.

####----------------------------------------------------------#
#### Voterfile loading/descriptives/analysis. 
####----------------------------------------------------------#



# Histograms, quantiles, prop tables, maps, etc. 
# TODO: 

# What state do you want to explore/analyze for 2024?
# TODO: 

####----------------------------------------------------------#
#### Simulation examples. 
####----------------------------------------------------------#




# Most demographic variables and turnout are not significant for Democrats, but they are for Republicans.
# Problem: we do not have demographic data for 2024. 
# What can we do? 
# A few options: 
# (1.) Estimate state-level demographics from voterfile and plug in for 2024. 
# (2.) Interpolate Census demographics using a spline or some type of model. 
# (3.) Simulate plausible values for variables based on historical averages or more advanced model. 











Citations
[1] - https://iop.harvard.edu/youth-poll/47th-edition-spring-2024
[] - as always, code borrowed from Teaching Fellow Matthew Dardet, check him out here - https://www.matthewdardet.com
