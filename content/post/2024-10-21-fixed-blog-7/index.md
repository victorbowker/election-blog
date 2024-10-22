---
title: "Fixed Blog 7"
author: "Victor Bowker"
date: "2024-10-19"
output:
  pdf_document: default
  blogdown::html_page: default
categories: []
tags: []
slug: "fixed-blog-7"
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

# Welcome Back!

Election day is *so soon* and I am overjoyed! There are so many things at stake, and I am excited to see the results. Today, I will focus on the **ground game**, which is everything a campaign does via the ground! This includes door knocking, holding signs at intersections, setting up field offices, giving out signs, and many more fun campaign activities! If you want to know whether the ground game matters, read on!

# The Countdown is ON!

Are you wondering how many days there are until the election? I know I am! Check below to see.

    ## Time difference of 14 days

# When Do Campaign Events Happen?

Have you ever been to a campaign event? Sometimes they are in big hotels, or small cafes, or even in the candidates home. They are created to bring voters together in support for the candidate. Sometimes, these are informal gatherings of top donors and supporters, created to rally funding around the candidate to hit vital funding goals. Other times, these are events to allow the candidate to show another side of themselves. They can be used to convince unlikely voters by establishing a true, one-on-one connection that is normally not found in large presidential campaigns. Finally, likely the largest, and most prominent, type of campaign event is the infamous rally! In key states, locals should not be surprised to pass large stages adorned with red, white, and blue.

Below, you will see the frequency of campaign events in the four months before the past 2 Presidential Elections, as well as the past three months of this cycle. You will not be at all surprised to see that campaign events always occur more often in the weeks leading up to the election. Candidates know there is always another vote they could receive, so they work tirelessly to mobilize voters in the final minutes before the big day. Check it out below!

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-33-1.png" width="672" />

# Where Are Campaign Events Happening?

Ready for something extra interesting? Below you will find a map of the United States of America. Atop the map of our lovely country are dots representing campaign events prior to a General Election. The dots reflect party. See anything fun? Hint: the right side of the country is *heavily* favored by campaign events. One thing you should note is the data for 2024 is not up to date by the day, so some more recent events are not included.

So, what states are receiving the most campaign attention? If you have been following the election, you may not be shocked to know states including Michigan, Wisconsin, North Carolina, Pennsylvania and Georgia are top contenders. See below!

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-35-1.png" width="672" />

# Prediction Time!

Okay okay time for the fun stuff. You will see below a regression table including last weeks data as well as an added coefficient for campaign events. I apologize that the term label is not updated to something cleaner than fun_campaign_events, but I had the darndest trouble trying to change it!

Alas, below you will see the data. Some key results are as follows. First, the September Polling results continue to be statistically significant in this situation. Next, October Results, which are only minorly significant in this prediction. Finally, the Campaign Events coefficient is not statistically significant. As you will see below, my prediction overall did not go well this week. This is certainly an allusion to that.

<div class="datatables html-widget html-fill-item" id="htmlwidget-1" style="width:100%;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"filter":"none","vertical":false,"caption":"<caption>Updated Regression Results<\/caption>","data":[["1","2","3","4"],["(Intercept)","September_Results","October_Results","fun_campaign_events"],[7.369536499685949,0.5926320724037712,0.239276137285784,0.2709500887186194],[6.709217476469807,0.1178869190284494,0.1405669349921378,0.2319711556171339],[1.09841967793293,5.027123257507072,1.702222057407507,1.168033534159824],[0.2744867906011789,2.012096064437448e-06,0.09161740857242563,0.2453892596035098]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>term<\/th>\n      <th>estimate<\/th>\n      <th>std.error<\/th>\n      <th>statistic<\/th>\n      <th>p.value<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"pageLength":4,"columnDefs":[{"className":"dt-right","targets":[2,3,4,5]},{"orderable":false,"targets":0},{"name":" ","targets":0},{"name":"term","targets":1},{"name":"estimate","targets":2},{"name":"std.error","targets":3},{"name":"statistic","targets":4},{"name":"p.value","targets":5}],"order":[],"autoWidth":false,"orderClasses":false,"lengthMenu":[4,10,25,50,100]},"selection":{"mode":"multiple","selected":null,"target":"row","selectable":null}},"evals":[],"jsHooks":[]}</script>

# Results: Do You Believe It??

Answer: I do not believe it. In this weeks prediction, you will see results for top swing states. Clearly, the lower and upper bounds of this prediction are *irregular* which I believe makes this prediction less than good science. I worked with my amazing classmate, Kaitlyn Vu, to try to correct these challenges, but was unable to do so. In any case, this is my prediction for the week!

<div id="xupzwgjgwt" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#xupzwgjgwt table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
&#10;#xupzwgjgwt thead, #xupzwgjgwt tbody, #xupzwgjgwt tfoot, #xupzwgjgwt tr, #xupzwgjgwt td, #xupzwgjgwt th {
  border-style: none;
}
&#10;#xupzwgjgwt p {
  margin: 0;
  padding: 0;
}
&#10;#xupzwgjgwt .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}
&#10;#xupzwgjgwt .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}
&#10;#xupzwgjgwt .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}
&#10;#xupzwgjgwt .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}
&#10;#xupzwgjgwt .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}
&#10;#xupzwgjgwt .gt_column_spanner_outer:first-child {
  padding-left: 0;
}
&#10;#xupzwgjgwt .gt_column_spanner_outer:last-child {
  padding-right: 0;
}
&#10;#xupzwgjgwt .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}
&#10;#xupzwgjgwt .gt_spanner_row {
  border-bottom-style: hidden;
}
&#10;#xupzwgjgwt .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}
&#10;#xupzwgjgwt .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}
&#10;#xupzwgjgwt .gt_from_md > :first-child {
  margin-top: 0;
}
&#10;#xupzwgjgwt .gt_from_md > :last-child {
  margin-bottom: 0;
}
&#10;#xupzwgjgwt .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}
&#10;#xupzwgjgwt .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}
&#10;#xupzwgjgwt .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}
&#10;#xupzwgjgwt .gt_row_group_first td {
  border-top-width: 2px;
}
&#10;#xupzwgjgwt .gt_row_group_first th {
  border-top-width: 2px;
}
&#10;#xupzwgjgwt .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}
&#10;#xupzwgjgwt .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_first_summary_row.thick {
  border-top-width: 2px;
}
&#10;#xupzwgjgwt .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}
&#10;#xupzwgjgwt .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}
&#10;#xupzwgjgwt .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}
&#10;#xupzwgjgwt .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}
&#10;#xupzwgjgwt .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}
&#10;#xupzwgjgwt .gt_left {
  text-align: left;
}
&#10;#xupzwgjgwt .gt_center {
  text-align: center;
}
&#10;#xupzwgjgwt .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}
&#10;#xupzwgjgwt .gt_font_normal {
  font-weight: normal;
}
&#10;#xupzwgjgwt .gt_font_bold {
  font-weight: bold;
}
&#10;#xupzwgjgwt .gt_font_italic {
  font-style: italic;
}
&#10;#xupzwgjgwt .gt_super {
  font-size: 65%;
}
&#10;#xupzwgjgwt .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}
&#10;#xupzwgjgwt .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}
&#10;#xupzwgjgwt .gt_indent_1 {
  text-indent: 5px;
}
&#10;#xupzwgjgwt .gt_indent_2 {
  text-indent: 10px;
}
&#10;#xupzwgjgwt .gt_indent_3 {
  text-indent: 15px;
}
&#10;#xupzwgjgwt .gt_indent_4 {
  text-indent: 20px;
}
&#10;#xupzwgjgwt .gt_indent_5 {
  text-indent: 25px;
}
&#10;#xupzwgjgwt .katex-display {
  display: inline-flex !important;
  margin-bottom: 0.75em !important;
}
&#10;#xupzwgjgwt div.Reactable > div.rt-table > div.rt-thead > div.rt-tr.rt-tr-group-header > div.rt-th-group:after {
  height: 0px !important;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="5" class="gt_heading gt_title gt_font_normal" style>Predicted Vote Share by State</td>
    </tr>
    <tr class="gt_heading">
      <td colspan="5" class="gt_heading gt_subtitle gt_font_normal gt_bottom_border" style>Including Confidence Intervals and Winner Prediction</td>
    </tr>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="state">State</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Prediction">Prediction</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Lower_Bound">Lower Bound</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" scope="col" id="Upper_Bound">Upper Bound</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="Winner">Winner</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="state" class="gt_row gt_left">Arizona</td>
<td headers="Prediction" class="gt_row gt_right">48.17</td>
<td headers="Lower_Bound" class="gt_row gt_right">17.84</td>
<td headers="Upper_Bound" class="gt_row gt_right">78.51</td>
<td headers="Winner" class="gt_row gt_left" style="background-color: #FF0000;">Trump</td></tr>
    <tr><td headers="state" class="gt_row gt_left">Georgia</td>
<td headers="Prediction" class="gt_row gt_right">49.09</td>
<td headers="Lower_Bound" class="gt_row gt_right">18.68</td>
<td headers="Upper_Bound" class="gt_row gt_right">79.50</td>
<td headers="Winner" class="gt_row gt_left" style="background-color: #FF0000;">Trump</td></tr>
    <tr><td headers="state" class="gt_row gt_left">Michigan</td>
<td headers="Prediction" class="gt_row gt_right">50.71</td>
<td headers="Lower_Bound" class="gt_row gt_right">20.07</td>
<td headers="Upper_Bound" class="gt_row gt_right">81.35</td>
<td headers="Winner" class="gt_row gt_left" style="background-color: #0000FF;">Harris</td></tr>
    <tr><td headers="state" class="gt_row gt_left">Nevada</td>
<td headers="Prediction" class="gt_row gt_right">48.36</td>
<td headers="Lower_Bound" class="gt_row gt_right">18.05</td>
<td headers="Upper_Bound" class="gt_row gt_right">78.68</td>
<td headers="Winner" class="gt_row gt_left" style="background-color: #FF0000;">Trump</td></tr>
    <tr><td headers="state" class="gt_row gt_left">North Carolina</td>
<td headers="Prediction" class="gt_row gt_right">49.37</td>
<td headers="Lower_Bound" class="gt_row gt_right">18.91</td>
<td headers="Upper_Bound" class="gt_row gt_right">79.82</td>
<td headers="Winner" class="gt_row gt_left" style="background-color: #FF0000;">Trump</td></tr>
    <tr><td headers="state" class="gt_row gt_left">Pennsylvania</td>
<td headers="Prediction" class="gt_row gt_right">50.88</td>
<td headers="Lower_Bound" class="gt_row gt_right">20.17</td>
<td headers="Upper_Bound" class="gt_row gt_right">81.59</td>
<td headers="Winner" class="gt_row gt_left" style="background-color: #0000FF;">Harris</td></tr>
    <tr><td headers="state" class="gt_row gt_left">Wisconsin</td>
<td headers="Prediction" class="gt_row gt_right">50.41</td>
<td headers="Lower_Bound" class="gt_row gt_right">19.94</td>
<td headers="Upper_Bound" class="gt_row gt_right">80.88</td>
<td headers="Winner" class="gt_row gt_left" style="background-color: #0000FF;">Harris</td></tr>
  </tbody>
  &#10;  
</table>
</div>

Citations - Assistance from Kaitlyn Vu with troubleshooting and code! - Chat GPT was used for the new table creation!
