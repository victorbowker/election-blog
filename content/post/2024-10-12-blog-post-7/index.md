---
title: Blog Post 6
author: Victor E. Bowker
date: '2024-10-12'
slug: blog-post-7
categories: []
tags: []
---

<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<link href="{{< blogdown/postref >}}index_files/datatables-css/datatables-crosstalk.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/datatables-binding/datatables.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery-3.6.0.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/dt-core/css/jquery.dataTables.min.css" rel="stylesheet" />
<link href="{{< blogdown/postref >}}index_files/dt-core/css/jquery.dataTables.extra.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/dt-core/js/jquery.dataTables.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>

<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

# Thanks for coming back

Welcome back! This is week 6, and I approve this message.
(get it?)

This week is all about campaign ads!!! Interestingly, my mention of campaign ads may cause groans from some, but others perhaps a mere nod; do you wonder why? Let me tell you!

Campaigns spend incredible amounts of money (NYT says 500 million will be spent between early September and Election Day) but this money is not allocated evenly across the country.\[1\] In the following graphs, I will first explain how campaigns allocate ad spending across states. Next, I will show you how the tone of these ads can differ. Then I will wrap up with some of my *favorite* campaign ads, then finally an update to my presidential projection!

Excited? Great, me too, so lets go!

# Ad Tone

Its safe to say that if you are interested enough in the election to read this blog then you probably have seen a campaign ad or two. In the case you have not, let me show you a somewhat hostile commercial released by the Biden Campaign, a few weeks prior to Biden’s stepping down from the race.

<iframe width="560" height="315" src="https://www.youtube.com/embed/MOEMX6_A8MM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>

Next, take a look at a non-hostile ad, from Senior Senator of New Hampshire, Jeanne Shaheen.

<iframe width="560" height="315" src="https://www.youtube.com/embed/W5nneOtfCXM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>

You can see the obvious differences between those two ads, right?
One is simply attacking the other candidate, reminding voters of past hostility and reasons to not vote for Fmr. President Trump. The second, Shaheen’s ad, is only touting her accomplishments, leveraging real voters to prove her lasting impact.

Below, you will see a breakdown of campaign ads in the Presidential race, between 2000 and 2012. The tone of each ad is presented as a percentage of total ads run by each party!

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />
*Figure 1*

# Do Ads Matter?

Now, after seeing some ads, and seeing how their tones vary, you may be wondering, do ads matter? There are a few historical examples that could shed some light on that question.

**Bush v. Dukakis**

In 1988, George H. W. Bush beat Michael Dukakis for President. The reasons for this outcome are numerous, but the one I’d like to draw your attention to is Bush’s attack ad campaigns.

Below you will see two ads, both attacking Dukakis on military support and crime, respectively. Dukakis himself reflected after the campaign and attributed his loss in great part to his campaign’s restraint with returning hostile ads towards Bush. \[2\]

*“Willie Horton”*

<iframe width="560" height="315" src="https://www.youtube.com/embed/cnxbRoHtiDE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>

*“Tank”*

<iframe width="560" height="315" src="https://www.youtube.com/embed/17k-kBpLwW0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>

**More Recent Times**

Attack ads don’t always work, however.
Below you will see an ad President Trump released before the 2018 midterms. Republicans lost the house in a big way during those elections…

*“The New Willie Horton Ad”*

<iframe width="560" height="315" src="https://www.youtube.com/embed/GQJx64cUFb8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>

Sometimes, ads don’t have to attack directly, but can take more subtle digs at the opponent. In the primaries of the 2008 Presidential Election, Fmr. Secretary of State Hillary Clinton released an ad, which I have attached below. As you may know, she did not win that race. Perhaps if it was more hostile towards then Senator Obama it would have worked? Who knows!

*“3am Call”*

<iframe width="560" height="315" src="https://www.youtube.com/embed/aZ_z9Tpdl9A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>

# Bang for your Buck: TV

When is the best time to purchase a time slot for an election? Is it months prior to November, when voters likely haven’t put much thought into their vote? Or is it more likely the weeks and days leading up that fateful Tuesday? See below, a visualization of when most ads spend is allocated!

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-13-1.png" width="672" />
*Figure 2*

# Bang for your Buck: Facebook

As in similar fashion to the TV ads seen above, Facebook also experiences some incredible increase in Ad Spend prior to the General Election. See below!

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-17-1.png" width="672" />
*Figure 3*

# Electoral College Prediction

Okay, regression time!
I have switched gears on my modelling, to now work on a Electoral College prediction based on state data! The below diagram (which is in a new fancy table model that StackOverflow helped me discover) shows the regression results for Dem candidates popular vote share state by state in August, September, and October! This also includes historical data averages from past election years in the same months.

<div class="datatables html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-1" style="width:100%;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"filter":"none","vertical":false,"caption":"<caption>Regression Results for State Model (1996-2020)<\/caption>","data":[["1","2","3"],["(Intercept)","September_Results","October_Results"],[7.688764853062181,-0.4148443625087502,1.360130719155099],[1.528722149372118,0.2047165283151798,0.1995313091757767],[5.029537157043309,-2.026433165523692,6.81662805087343],[7.986236710074317e-07,0.04350296860134854,4.277889360760009e-11]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>term<\/th>\n      <th>estimate<\/th>\n      <th>std.error<\/th>\n      <th>statistic<\/th>\n      <th>p.value<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"pageLength":4,"columnDefs":[{"className":"dt-right","targets":[2,3,4,5]},{"orderable":false,"targets":0},{"name":" ","targets":0},{"name":"term","targets":1},{"name":"estimate","targets":2},{"name":"std.error","targets":3},{"name":"statistic","targets":4},{"name":"p.value","targets":5}],"order":[],"autoWidth":false,"orderClasses":false,"lengthMenu":[4,10,25,50,100]},"selection":{"mode":"multiple","selected":null,"target":"row","selectable":null}},"evals":[],"jsHooks":[]}</script>

**Analysis**

First off, September seems to have little significance in the projection, while October has great significance! It appears that a 1% increase in October polling reflects a 1.3% increase in Dem popular vote share-how fun!!

The r-squared is high! Great sign. That means this is roughly 86% accurate at predicting the two-party vote share for Dems, state by state.

# Toss Up States!


Okay quick prediction time. In the below table you will see that Harris wins most of the toss up states, except Minnesota, New Hampshire, New Mexico, and Virginia. These projections are not completely in line with most online projections, so I am not fully confident in this diagnosis. Considering this projection has Harris winning Texas and Florida, I am not too confident in this projection. But, for this week, we have Harris winning!

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
State
</th>
<th style="text-align:right;">
Prediction
</th>
<th style="text-align:right;">
Lower Bound
</th>
<th style="text-align:right;">
Upper Bound
</th>
<th style="text-align:left;">
Winner
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;background-color: DARKBLUE !important;">
Arizona
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
53.49
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
43.22
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
63.75
</td>
<td style="text-align:left;background-color: DARKBLUE !important;">
Harris
</td>
</tr>
<tr>
<td style="text-align:left;background-color: DARKBLUE !important;">
Florida
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
54.84
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
44.57
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
65.11
</td>
<td style="text-align:left;background-color: DARKBLUE !important;">
Harris
</td>
</tr>
<tr>
<td style="text-align:left;background-color: DARKBLUE !important;">
Georgia
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
53.67
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
43.41
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
63.93
</td>
<td style="text-align:left;background-color: DARKBLUE !important;">
Harris
</td>
</tr>
<tr>
<td style="text-align:left;background-color: DARKBLUE !important;">
Michigan
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
51.70
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
41.44
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
61.96
</td>
<td style="text-align:left;background-color: DARKBLUE !important;">
Harris
</td>
</tr>
<tr>
<td style="text-align:left;background-color: darkred !important;">
Minnesota
</td>
<td style="text-align:right;background-color: darkred !important;">
49.65
</td>
<td style="text-align:right;background-color: darkred !important;">
39.39
</td>
<td style="text-align:right;background-color: darkred !important;">
59.91
</td>
<td style="text-align:left;background-color: darkred !important;">
Trump
</td>
</tr>
<tr>
<td style="text-align:left;background-color: DARKBLUE !important;">
Nevada
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
52.10
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
41.83
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
62.36
</td>
<td style="text-align:left;background-color: DARKBLUE !important;">
Harris
</td>
</tr>
<tr>
<td style="text-align:left;background-color: darkred !important;">
New Hampshire
</td>
<td style="text-align:right;background-color: darkred !important;">
49.51
</td>
<td style="text-align:right;background-color: darkred !important;">
39.25
</td>
<td style="text-align:right;background-color: darkred !important;">
59.78
</td>
<td style="text-align:left;background-color: darkred !important;">
Trump
</td>
</tr>
<tr>
<td style="text-align:left;background-color: darkred !important;">
New Mexico
</td>
<td style="text-align:right;background-color: darkred !important;">
47.42
</td>
<td style="text-align:right;background-color: darkred !important;">
37.16
</td>
<td style="text-align:right;background-color: darkred !important;">
57.68
</td>
<td style="text-align:left;background-color: darkred !important;">
Trump
</td>
</tr>
<tr>
<td style="text-align:left;background-color: DARKBLUE !important;">
North Carolina
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
53.39
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
43.13
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
63.66
</td>
<td style="text-align:left;background-color: DARKBLUE !important;">
Harris
</td>
</tr>
<tr>
<td style="text-align:left;background-color: DARKBLUE !important;">
Pennsylvania
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
52.61
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
42.35
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
62.88
</td>
<td style="text-align:left;background-color: DARKBLUE !important;">
Harris
</td>
</tr>
<tr>
<td style="text-align:left;background-color: DARKBLUE !important;">
Texas
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
55.69
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
45.43
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
65.96
</td>
<td style="text-align:left;background-color: DARKBLUE !important;">
Harris
</td>
</tr>
<tr>
<td style="text-align:left;background-color: darkred !important;">
Virginia
</td>
<td style="text-align:right;background-color: darkred !important;">
48.65
</td>
<td style="text-align:right;background-color: darkred !important;">
38.39
</td>
<td style="text-align:right;background-color: darkred !important;">
58.91
</td>
<td style="text-align:left;background-color: darkred !important;">
Trump
</td>
</tr>
<tr>
<td style="text-align:left;background-color: DARKBLUE !important;">
Wisconsin
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
52.25
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
41.99
</td>
<td style="text-align:right;background-color: DARKBLUE !important;">
62.51
</td>
<td style="text-align:left;background-color: DARKBLUE !important;">
Harris
</td>
</tr>
</tbody>
</table>

\# Citations

\[1\] - https://www.nytimes.com/2024/09/17/us/elections/presidential-campaign-advertising-spending.html

\[2\] - https://www.politico.com/magazine/gallery/2013/11/how-bush-beat-dukakis-000005/?slide=0

\[3\] - Kaitlyn Vu! She is great. Check our her blog here: https://kaitvu.github.io/election-blog/post/2024/10/09/blog-6/
