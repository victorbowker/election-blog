---
title: "Blog Post 7"
author: "Victor Bowker"
date: "2024-10-19"
output:
  pdf_document: default
  blogdown::html_page: default
categories: []
tags: []
slug: "7th-blog-post"
---


# Welcome Back!

Election day is *so soon* and I am overjoyed! There are so many things at stake, and I am excited to see the results. Today, I will focus on the **ground game**, which is everything a campaign does via the ground! This includes door knocking, holding signs at intersections, setting up field offices, giving out signs, and many more fun campaign activities! If you want to know whether the ground game matters, read on!

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
options(repos = c(CRAN = "https://cloud.r-project.org"))

```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
install.packages("patchwork")
library(patchwork)
library(broom)
library(geofacet)
library(ggpubr)
library(ggthemes)
library(haven)
library(DT)
library(kableExtra)
library(maps)
library(mgcv)
library(mgcViz)
library(RColorBrewer)
library(scales)
library(sf)
library(spData)
library(stargazer)
library(tidygeocoder)
library(tidyverse)
library(tigris)
library(tmap)
library(tmaptools)
library(viridis)
library(tidyverse)
library(gt)
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Read popular vote datasets. 
d_popvote <- read_csv("popvote_1948_2020.csv")
d_state_popvote <- read_csv("state_popvote_1948_2020.csv")
d_state_popvote[d_state_popvote$state == "District of Columbia",]$state <- "District Of Columbia"
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Read elector distribution dataset. 
d_ec <- read_csv("corrected_ec_1948_2024.csv")
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Read polling data. 
d_polls <- read_csv("national_polls_1968-2024.csv")
d_state_polls <- read_csv("state_polls_1968-2024.csv")
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Read turnout data. 
d_turnout <- read_csv("state_turnout_1980_2022.csv")
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Read county turnout. 
d_county_turnout <- read_csv("county_turnout.csv")
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Read state-level demographics.
d_state_demog <- read_csv("demographics.csv")
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Read county demographics. 
d_county_demog <- read_csv("county_demographics.csv")
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Read campaign events datasets. 
d_campaign_events <- read_csv("campaigns_2016_2024.csv")[,-1]
```

# The Countdown is ON!

Are you wondering how many days there are until the election? I know I am! Check below to see.

```{r, echo=FALSE, warning=FALSE, message=FALSE}
# How many days until the election? 
election.day <- as.Date("2024-11-05")
current.date <- Sys.Date()

election.day-current.date
# 20 days!!!!!!
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Merge popular vote and polling data. 
d <- d_state_popvote |> 
  inner_join(d_state_polls |> filter(weeks_left == 3)) |> 
  mutate(state_abb = state.abb[match(state, state.name)])
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Generate state-specific univariate poll-based forecasts with linear model.
state_forecast <- list()
state_forecast_outputs <- data.frame()
for (s in unique(d$state_abb)) {
  # Democrat model.
  state_forecast[[s]]$dat_D <- d |> filter(state_abb == s, party == "DEM")
  state_forecast[[s]]$mod_D <- lm(D_pv ~ poll_support, 
                                  state_forecast[[s]]$dat_D)
  
  # Republican model.
  state_forecast[[s]]$dat_R <- d |> filter(state_abb == s, party == "REP")
  state_forecast[[s]]$mod_R <- lm(R_pv ~ poll_support, 
                                  state_forecast[[s]]$dat_R)
  
  if (nrow(state_forecast[[s]]$dat_R) > 2) {
    # Save state-level model estimates. 
    state_forecast_outputs <- rbind(state_forecast_outputs, 
                                    rbind(cbind.data.frame(
                                      intercept = summary(state_forecast[[s]]$mod_D)$coefficients[1,1], 
                                      intercept_se = summary(state_forecast[[s]]$mod_D)$coefficients[1,2],
                                      slope = summary(state_forecast[[s]]$mod_D)$coefficients[2,1], 
                                      state_abb = s, 
                                      party = "DEM"), 
                                    rbind(cbind.data.frame(
                                     intercept = summary(state_forecast[[s]]$mod_R)$coefficients[1,1],
                                     intercept_se = summary(state_forecast[[s]]$mod_R)$coefficients[1,2],
                                     slope = summary(state_forecast[[s]]$mod_R)$coefficients[2,1],
                                     state_abb = s,
                                     party = "REP"
                                    ))))
  }
}
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Make graphs of polls in different states/parties at different levels of strength/significance of outcome. 
state_forecast_trends <- state_forecast_outputs |> 
  mutate(`0` = intercept, 
         `25` = intercept + slope*25, 
         `50` = intercept + slope*50, 
         `75` = intercept + slope*75, 
         `100` = intercept + slope*100) |>
  select(-intercept, -slope) |> 
  gather(x, y, -party, -state_abb, -intercept_se) |> 
  mutate(x = as.numeric(x))
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Q: What's wrong with this map? 
# A: (1.) no polls in some states
#    (2.) very high variance for some states (Nevada)/negative slopes for others (Mississippi)
#    (3.) y is not always in the [0, 100] range
ggplot(state_forecast_trends, aes(x=x, y=y, ymin=y-intercept_se, ymax=y+intercept_se)) + 
  facet_geo(~ state_abb) +
  geom_line(aes(color = party)) + 
  geom_ribbon(aes(fill = party), alpha=0.5, color=NA) +
  coord_cartesian(ylim=c(0, 100)) +
  scale_color_manual(values = c("blue", "red")) +
  scale_fill_manual(values = c("blue", "red")) +
  xlab("Hypothetical Poll Support") +
  ylab("Predicted Voteshare\n(pv = A + B * poll)") +
  ggtitle("") +
  theme_bw()

state_forecast_trends |>
  filter(state_abb == "CA" | state_abb == "FL")|>
  ggplot(aes(x=x, y=y, ymin=y-intercept_se, ymax=y+intercept_se)) + 
  facet_wrap(~ state_abb) +
  geom_line(aes(color = party)) + 
  geom_hline(yintercept = 100, lty = 3) +
  geom_hline(yintercept = 0, lty = 3) + 
  geom_ribbon(aes(fill = party), alpha=0.5, color=NA) +
  ## N.B. You can, in fact, combine *different* data and aesthetics
  ##       in one ggplot; but this usually needs to come at the end 
  ##       and you must explicitly override all previous aesthetics
  geom_text(data = d |> filter(state_abb == "CA", party=="DEM"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  geom_text(data = d |> filter(state_abb == "CA", party=="REP"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  geom_text(data = d |> filter(state_abb == "FL", party=="DEM"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  geom_text(data = d |> filter(state_abb == "FL", party=="REP"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  scale_color_manual(values = c("blue", "red")) +
  scale_fill_manual(values = c("blue", "red")) +
  xlab("Hypothetical Poll Support") +
  ylab("Predicted Voteshare\n(pv = A + B * poll)") +
  theme_bw()
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Merge turnout data into main dataset. 
d <- d |> 
  left_join(d_turnout, by = c("state", "year")) |> 
  filter(year >= 1980) # Filter to when turnout dataset begins. 

# Generate probabilistic univariate poll-based state forecasts. 
state_glm_forecast <- list()
state_glm_forecast_outputs <- data.frame()
for (s in unique(d$state_abb)) {
  # Democrat model. 
  state_glm_forecast[[s]]$dat_D <- d |> filter(state_abb == s, party == "DEM")
  state_glm_forecast[[s]]$mod_D <- glm(cbind(votes_D, vep - votes_D) ~ poll_support, # Cbind(N Success, N Total) for Binomial Model 
                                      state_glm_forecast[[s]]$dat_D, 
                                      family = binomial(link = "logit"))
  
  # Republican model. 
  state_glm_forecast[[s]]$dat_R <- d |> filter(state_abb == s, party == "REP")
  state_glm_forecast[[s]]$mod_R <- glm(cbind(votes_R, vep - votes_R) ~ poll_support, 
                                      state_glm_forecast[[s]]$dat_R, 
                                      family = binomial(link = "logit"))
  
  if (nrow(state_glm_forecast[[s]]$dat_R) > 2) {
    for (hypo_avg_poll in seq(from = 0, to = 100, by = 10)) { 
      # Democrat prediction. 
      D_pred_vote_prob <- predict(state_glm_forecast[[s]]$mod_D, 
                                  newdata = data.frame(poll_support = hypo_avg_poll), se = TRUE, type = "response")
      D_pred_qt <- qt(0.975, df = df.residual(state_glm_forecast[[s]]$mod_D)) # Used in the prediction interval formula. 
      
      # Republican prediction. 
      R_pred_vote_prob <- predict(state_glm_forecast[[s]]$mod_R, 
                                  newdata = data.frame(poll_support = hypo_avg_poll), se = TRUE, type = "response")
      R_pred_qt <- qt(0.975, df = df.residual(state_glm_forecast[[s]]$mod_R)) # Used in the prediction interval formula.
      
      # Save predictions. 
      state_glm_forecast_outputs <- rbind(state_glm_forecast_outputs, 
                                          cbind.data.frame(x = hypo_avg_poll,
                                                           y = D_pred_vote_prob$fit*100,
                                                           ymin = (D_pred_vote_prob$fit - D_pred_qt*D_pred_vote_prob$se.fit)*100,
                                                           ymax = (D_pred_vote_prob$fit + D_pred_qt*D_pred_vote_prob$se.fit)*100,
                                                           state_abb = s, 
                                                           party = "DEM"),
                                          cbind.data.frame(x = hypo_avg_poll,
                                                           y = R_pred_vote_prob$fit*100,
                                                           ymin = (R_pred_vote_prob$fit - R_pred_qt*R_pred_vote_prob$se.fit)*100,
                                                           ymax = (R_pred_vote_prob$fit + R_pred_qt*R_pred_vote_prob$se.fit)*100,
                                                           state_abb = s, 
                                                           party = "REP"))
    }
  }
}
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Make graphs of polls in different states/parties at different levels of strength/significance of outcome. 
ggplot(state_glm_forecast_outputs, aes(x=x, y=y, ymin=ymin, ymax=ymax)) + 
  facet_geo(~ state_abb) +
  geom_line(aes(color = party)) + 
  geom_ribbon(aes(fill = party), alpha=0.5, color=NA) +
  coord_cartesian(ylim=c(0, 100)) +
  scale_color_manual(values = c("blue", "red")) +
  scale_fill_manual(values = c("blue", "red")) +
  xlab("Hypothetical Poll Support") +
  ylab('Probability of State-Eligible Voter Voting for Party') +
  theme_bw()

state_glm_forecast_outputs |>
  filter(state_abb == "CA" | state_abb == "FL") |>
  ggplot(aes(x=x, y=y, ymin=ymin, ymax=ymax)) + 
  facet_wrap(~ state_abb) +
  geom_line(aes(color = party)) + 
  geom_ribbon(aes(fill = party), alpha=0.5, color=NA) +
  coord_cartesian(ylim=c(0, 100)) +
  geom_text(data = d |> filter(state_abb == "CA", party=="DEM"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  geom_text(data = d |> filter(state_abb == "CA", party=="REP"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  geom_text(data = d |> filter(state_abb == "FL", party=="DEM"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  geom_text(data = d |> filter(state_abb == "FL", party=="REP"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  scale_color_manual(values = c("blue", "red")) +
  scale_fill_manual(values = c("blue", "red")) +
  xlab("Hypothetical Poll Support") +
  ylab('Probability of\nState-Eligible Voter\nVoting for Party') +
  ggtitle("Binomial Logit") + 
  theme_bw() + 
  theme(axis.title.y = element_text(size=6.5))
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Simulating a distribution of potential election results in Pennsylvania for 2024. 
# First step. Let's use GAM (general additive model) to impute VEP in Pennsylvania for 2024 using historical VEP.

# Get historical eligible voting population in Pennsylvania. 
vep_PA_2020 <- as.integer(d_turnout$vep[d_turnout$state == "Pennsylvania" & d_turnout$year == 2020])
vep_PA <- d_turnout |> filter(state == "Pennsylvania") |> select(vep, year)
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Fit regression for 2024 VEP prediction. 
lm_vep_PA <- lm(vep ~ year, vep_PA)

plot(x = vep_PA$year, y = vep_PA$vep, xlab = "Year", ylab = "VEP", main = "Voting Eligible Population in Pennsylvania by Year")
abline(lm_vep_PA, col = "red")

vep_PA_2024_ols <- predict(lm_vep_PA, newdata = data.frame(year = 2024)) |> as.numeric()

gam_vep_PA <- mgcv::gam(vep ~ s(year), data = vep_PA)
print(plot(getViz(gam_vep_PA)) + l_points() + l_fitLine(linetype = 3) + l_ciLine(colour = 2) + theme_get()) 
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Use generalized additive model (GAM) to predict 2024 VEP in Pennsylvania.
vep_PA_2024_gam <- predict(gam_vep_PA, newdata = data.frame(year = 2024)) |> as.numeric()
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Take weighted average of linear and GAM predictions for final prediction. 
vep_PA_2024 <- as.integer(0.75*vep_PA_2024_gam + 0.25*vep_PA_2024_ols)
vep_PA_2024
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Split datasets by party. 
PA_D <- d |> filter(state == "Pennsylvania" & party == "DEM")
PA_R <- d |> filter(state == "Pennsylvania" & party == "REP")
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Fit Democrat and Republican models. 
PA_D_glm <- glm(cbind(votes_R, vep - votes_R) ~ poll_support, data = PA_D, family = binomial(link = "logit"))
PA_R_glm <- glm(cbind(votes_R, vep - votes_R) ~ poll_support, data = PA_R, family = binomial(link = "logit"))
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Get predicted draw probabilities for D and R. 
(PA_pollav_D <- d_state_polls$poll_support[d_state_polls$state == "Pennsylvania" & d_state_polls$weeks_left == 3 & d_state_polls$party == "DEM"] |> mean(na.rm = T))
(PA_pollav_R <- d_state_polls$poll_support[d_state_polls$state == "Pennsylvania" & d_state_polls$weeks_left == 3 & d_state_polls$party == "REP"] |> mean(na.rm = T))
(PA_sdpoll_D <- sd(d_state_polls$poll_support[d_state_polls$state == "Pennsylvania" & d_state_polls$weeks_left == 3 & d_state_polls$party == "DEM"] |> na.omit()))
(PA_sdpoll_R <- sd(d_state_polls$poll_support[d_state_polls$state == "Pennsylvania" & d_state_polls$weeks_left == 3 & d_state_polls$party == "REP"] |> na.omit()))

(prob_D_vote_PA_2024 <- predict(PA_D_glm, newdata = data.frame(poll_support = PA_pollav_D), se = TRUE, type = "response")[[1]] |> as.numeric())
(prob_R_vote_PA_2024 <- predict(PA_R_glm, newdata = data.frame(poll_support = PA_pollav_R), se = TRUE, type = "response")[[1]] |> as.numeric())
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Get predicted distribution of draws from the population. 
sim_D_votes_PA_2024 <- rbinom(n = 10000, size = vep_PA_2024, prob = prob_D_vote_PA_2024)
sim_R_votes_PA_2024 <- rbinom(n = 10000, size = vep_PA_2024, prob = prob_R_vote_PA_2024)
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Simulating a distribution of election results: Harris PA PV. 
hist(sim_D_votes_PA_2024, breaks = 100, col = "blue", main = "Predicted Turnout Draws for Harris \n from 10,000 Binomial Process Simulations")
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Simulating a distribution of election results: Trump PA PV. 
hist(sim_R_votes_PA_2024, breaks = 100, col = "red", main = "Predicted Turnout Draws for Trump \n from 10,000 Binomial Process Simulations")
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Simulating a distribution of election results: Trump win margin. 
sim_elxns_PA_2024 <- ((sim_R_votes_PA_2024-sim_D_votes_PA_2024)/(sim_D_votes_PA_2024 + sim_R_votes_PA_2024))*100
hist(sim_elxns_PA_2024, breaks = 100, col = "firebrick1", main = "Predicted Draws of Win Margin for Trump \n from 10,000 Binomial Process Simulations", xlim = c(0, 0.4))
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Simulations incorporating prior for SD. 
sim_D_votes_PA_2024_2 <- rbinom(n = 10000, size = vep_PA_2024, prob = rnorm(10000, PA_pollav_D/100, PA_sdpoll_D/100))
sim_R_votes_PA_2024_2 <- rbinom(n = 10000, size = vep_PA_2024, prob = rnorm(10000, PA_pollav_R/100, PA_sdpoll_R/100))
sim_elxns_PA_2024_2 <- ((sim_R_votes_PA_2024_2-sim_D_votes_PA_2024_2)/(sim_D_votes_PA_2024_2 + sim_R_votes_PA_2024_2))*100
h <- hist(sim_elxns_PA_2024_2, breaks = 100, col = "firebrick1")
cuts <- cut(h$breaks, c(-Inf, 0, Inf))
plot(h, yaxt = "n", bty = "n", xlab = "", ylab = "", main = "", xlim = c(-35, 35), col = c("blue", "red")[cuts], cex.axis=0.8)
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Where should campaigns build field offices? 
fo_2012 <- read_csv("fieldoffice_2012_bycounty.csv")

lm_obama <- lm(obama12fo ~ romney12fo + 
                 swing + 
                 core_rep + 
                 swing:romney12fo + 
                 core_rep:romney12fo + 
                 battle + 
                 medage08 + 
                 pop2008 + 
                 pop2008^2 + 
                 medinc08 + 
                 black + 
                 hispanic + 
                 pc_less_hs00 + 
                 pc_degree00 + 
                 as.factor(state), 
               fo_2012)

lm_romney <- lm(romney12fo ~ 
                  obama12fo + 
                  swing + 
                  core_dem + 
                  swing:obama12fo + 
                  core_dem:obama12fo + 
                  battle + 
                  medage08 + 
                  pop2008 + 
                  pop2008^2 + 
                  medinc08 + 
                  black + 
                  hispanic + 
                  pc_less_hs00 + 
                  pc_degree00 + 
                  as.factor(state),
                  fo_2012)

stargazer(lm_obama, lm_romney, header=FALSE, type='latex', no.space = TRUE,
          column.sep.width = "3pt", font.size = "scriptsize", single.row = TRUE,
          keep = c(1:7, 62:66), omit.table.layout = "sn",
          title = "Placement of Field Offices (2012)")
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Effects of field offices on turnout and vote share. 
fo_dem <- read_csv("fieldoffice_2004-2012_dems.csv")

ef_t <- lm(turnout_change ~ dummy_fo_change + battle + dummy_fo_change:battle + as.factor(state) + as.factor(year), fo_dem)

ef_d <- lm(dempct_change ~ dummy_fo_change + battle + dummy_fo_change:battle + as.factor(state) + as.factor(year), fo_dem)

stargazer(ef_t, ef_d, header=FALSE, type='latex', no.space = TRUE,
          column.sep.width = "3pt", font.size = "scriptsize", single.row = TRUE,
          keep = c(1:3, 53:54), keep.stat = c("n", "adj.rsq", "res.dev"),
          title = "Effect of DEM Field Offices on Turnout and DEM Vote Share (2004-2012)")
```

```{r, include=FALSE, echo=FALSE, warning=FALSE, message=FALSE}
# Field Strategies of Obama, Romney, Clinton, and Trump in 2016. 
fo_add <- read_csv("fieldoffice_2012-2016_byaddress.csv")


```

# When Do Campaign Events Happen?

Have you ever been to a campaign event? Sometimes they are in big hotels, or small cafes, or even in the candidates home. They are created to bring voters together in support for the candidate. Sometimes, these are informal gatherings of top donors and supporters, created to rally funding around the candidate to hit vital funding goals. Other times, these are events to allow the candidate to show another side of themselves. They can be used to convince unlikely voters by establishing a true, one-on-one connection that is normally not found in large presidential campaigns. Finally, likely the largest, and most prominent, type of campaign event is the infamous rally! In key states, locals should not be surprised to pass large stages adorned with red, white, and blue.

Below, you will see the frequency of campaign events in the four months before the past 2 Presidential Elections, as well as the past three months of this cycle. You will not be at all surprised to see that campaign events always occur more often in the weeks leading up to the election. Candidates know there is always another vote they could receive, so they work tirelessly to mobilize voters in the final minutes before the big day. Check it out below!

```{r, echo=FALSE, warning=FALSE, message=FALSE}
# Clinton 2016 Field Offices - Obama 2008 Field Offices. 



# Case Study: Wisconsin Field Offices in 2012 and 2016 



# Visualizing campaign events. 
d_campaign_events$party[d_campaign_events$candidate %in% c("Trump / Pence", "Trump", "Pence", "Trump/Pence", "Vance")] <- "REP"
d_campaign_events$party[d_campaign_events$candidate %in% c("Biden / Harris", "Biden", "Harris", "Biden/Harris", "Walz", "Kaine", "Clinton", "Clinton / Kaine")] <- "DEM"
p.ev.1 <- d_campaign_events |> 
  group_by(date, party) |> 
  summarize(n_events = n(), year) |> 
  filter(year == 2016) |> 
  ggplot(aes(x = date, y = n_events, color = party)) + 
          geom_point(alpha = 0.7, size = 1, position = position_jitter(width = 0.2)) +  
        geom_smooth() + 
        ggtitle("Campaign Events Leading Up To General Elections") + 
        xlab("Date") +
        ylab("Number of Events") +
        scale_color_manual(values = c("DEM" = "dodgerblue2", "REP" = "firebrick2")) +
        labs(subtitle = "2016")

p.ev.2 <- d_campaign_events |> 
  group_by(date, party) |> 
  summarize(n_events = n(), year) |> 
  filter(year == 2020) |> 
      ggplot(aes(x = date, y = n_events, color = party)) + 
          geom_point(alpha = 0.7, size = 1, position = position_jitter(width = 0.2)) +  
        geom_smooth() + 
        ggtitle(" ") + 
        xlab(" ") +
        ylab(" ") +
        scale_color_manual(values = c("DEM" = "dodgerblue2", "REP" = "firebrick2")) +
        labs(subtitle = "2020")


p.ev.3 <- d_campaign_events |> 
  group_by(date, party) |> 
summarize(n_events = n(), year) |> 
  filter(year == 2024) |> 
        ggplot(aes(x = date, y = n_events, color = party)) + 
          geom_point(alpha = 0.7, size = 1, position = position_jitter(width = 0.2)) +  
        geom_smooth() + 
        ggtitle(" ") + 
        xlab(" ") +
        ylab(" ") +
        scale_color_manual(values = c("DEM" = "dodgerblue2", "REP" = "firebrick2")) +
        labs(subtitle = "2024")

ggarrange(p.ev.1, p.ev.2, p.ev.3, ncol = 1, nrow = 3)
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
# Mapping campaign events. 


d_campaign_events <- read_csv("campaign_events_geocoded.csv")
d_campaign_events$party[d_campaign_events$candidate %in% c("Trump / Pence", "Trump", "Pence", "Trump/Pence", "Vance")] <- "REP"
d_campaign_events$party[d_campaign_events$candidate %in% c("Biden / Harris", "Biden", "Harris", "Biden/Harris", "Walz", "Kaine", "Clinton", "Clinton / Kaine")] <- "DEM"

us_geo <- states(cb = TRUE) |> 
  shift_geometry() |> 
  filter(STUSPS %in% unique(fo_add$state))

d_campaign_events <- d_campaign_events |> 
  filter(between(longitude, -180, -60), between(latitude, 20, 72))

d_ev_transformed <- st_as_sf(d_campaign_events |> 
                               drop_na(), coords = c("longitude", "latitude"), crs = 4326) |>
  st_transform(crs = st_crs(us_geo)) |>
  shift_geometry() |> 
  st_make_valid()

ev16 <- ggplot() +
  geom_sf(data = us_geo, fill = "gray95", color = "black", size = 0.5) +  
  geom_sf(data = d_ev_transformed |> 
            filter(year == 2016), aes(color = party), size = 2, alpha = 0.6) +
  ggtitle("2016") +
  labs(subtitle = " ") +
  scale_color_manual(values = c("DEM" = "blue", "REP" = "red")) +  
  theme(legend.position = "bottom", legend.title = element_text(size = 10),
        legend.text = element_text(size = 8)) +
  theme_void() +
    theme(legend.position = "bottom", 
        legend.title = element_text(size = 10), 
        legend.text = element_text(size = 8),
        plot.title = element_text(hjust = 0.5, size = 16, face = "bold"),  
        plot.subtitle = element_text(hjust = 0.5, size = 12))   

ev20 <- ggplot() +
  geom_sf(data = us_geo, fill = "gray95", color = "black", size = 0.5) +  
  geom_sf(data = d_ev_transformed |> 
            filter(year == 2020), aes(color = party), size = 2, alpha = 0.6) +
  ggtitle("2020") +
  labs(subtitle = " ") +
  scale_color_manual(values = c("DEM" = "blue", "REP" = "red")) +  
  theme(legend.position = "bottom", legend.title = element_text(size = 10),
        legend.text = element_text(size = 8)) +
  theme_void() +
    theme(legend.position = "bottom", 
        legend.title = element_text(size = 10), 
        legend.text = element_text(size = 8),
        plot.title = element_text(hjust = 0.5, size = 16, face = "bold"),  
        plot.subtitle = element_text(hjust = 0.5, size = 12))   

ev24 <- ggplot() +
  geom_sf(data = us_geo, fill = "gray95", color = "black", size = 0.5) +  
  geom_sf(data = d_ev_transformed |> 
            filter(year == 2024), aes(color = party), size = 2, alpha = 0.6) +
  ggtitle("2024") +
  labs(subtitle = " ") +
  scale_color_manual(values = c("DEM" = "blue", "REP" = "red")) +  
  theme(legend.position = "bottom", legend.title = element_text(size = 10),
        legend.text = element_text(size = 8)) +
  theme_void() +
    theme(legend.position = "bottom", 
        legend.title = element_text(size = 10), 
        legend.text = element_text(size = 8),
        plot.title = element_text(hjust = 0.5, size = 16, face = "bold"), 
        plot.subtitle = element_text(hjust = 0.5, size = 12)) 




```

# Where Are Campaign Events Happening?

Ready for something extra interesting? Below you will find a map of the United States of America. Atop the map of our lovely country are dots representing campaign events prior to a General Election. The dots reflect party. See anything fun? Hint: the right side of the country is *heavily* favored by campaign events. One thing you should note is the data for 2024 is not up to date by the day, so some more recent events are not included.

So, what states are receiving the most campaign attention? If you have been following the election, you may not be shocked to know states including Michigan, Wisconsin, North Carolina, Pennsylvania and Georgia are top contenders. See below!

```{r, echo=FALSE, warning=FALSE, message=FALSE}
# Load the patchwork library to combine ggplots
library(patchwork)

ev16 <- ev16 + theme(legend.position = "none")
ev20 <- ev20 + theme(legend.position = "bottom")
ev24 <- ev24 + theme(legend.position = "none")

combined_plot_side_by_side <- ev16 + ev20 + ev24 + 
  plot_layout(ncol = 3) +  # Combine into one row (side by side)
  plot_annotation(
    title = "Location of Campaign Events (2016-2024)",
    theme = theme(
      plot.title = element_text(hjust = 0.5, size = 18, face = "bold")
    )
  )

# Display the combined plot
combined_plot_side_by_side

```



```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}

state_abb_xwalk <- d_state_popvote |>
  mutate(state_abb = state.abb[match(d_state_popvote$state, state.name)]) |> 
  select(state, state_abb) |> 
  distinct() 
state_abb_xwalk[51,]$state <- "District Of Columbia"
state_abb_xwalk[51,]$state_abb <- "DC"
```



```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
d_campaign_events <-
  d_campaign_events |>
  rename("state_abb" = "state")
```



```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
kaitlyn_dataset <- 
  d_campaign_events |> 
  filter(party == "DEM") |>
  left_join(state_abb_xwalk, by = "state_abb") |> 
  left_join(d_state_popvote, by = c("state", "year")) |>
  group_by(state, year) |>
  summarize(fun_campaign_events = n()) 
```



```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
library(dplyr)
library(tidyr)
library(lubridate)

model44 <- d_state_polls |>
  select(state, year, weeks_left, poll_date, poll_support, party) |>
  filter(month(as.Date(poll_date)) %in% c(9, 10), party == "DEM", year >= 2016) |>
  filter(year < 2024) |>
  group_by(year, state, month = month(as.Date(poll_date))) |>
  summarize(poll_support = round(weighted.mean(poll_support, weeks_left, na.rm = TRUE), 3), .groups = "drop") |>
  pivot_wider(names_from = month, 
              values_from = poll_support, 
              names_prefix = "month_") |>
  left_join(d_state_popvote, by = c("year", "state")) |>
  select(year,state, month_9, month_10, D_pv2p) |>
  rename(September_Results = month_9, 
         October_Results = month_10) |>
  left_join(kaitlyn_dataset, by = c("state", "year")) |>
  mutate(across(everything(), ~ replace_na(., 0))) 


```


```{r, echo=FALSE, warning=FALSE, include=FALSE, message=FALSE}
reg44 <- lm(D_pv2p ~ September_Results + October_Results + fun_campaign_events, 
                data = model44)
```

# Prediction Time!

Okay okay time for the fun stuff. You will see below a regression table including last weeks data as well as an added coefficient for campaign events. I apologize that the term label is not updated to something cleaner than fun_campaign_events, but I had the darndest trouble trying to change it!

Alas, below you will see the data. Some key results are as follows. First, the September Polling results continue to be statistically significant in this situation. Next, October Results, which are only minorly significant in this prediction. Finally, the Campaign Events coefficient is not statistically significant. As you will see below, my prediction overall did not go well this week. This is certainly an allusion to that.

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
tidy_model44 <- tidy(reg44)
```

```{r, echo=FALSE, warning=FALSE, message=FALSE}
datatable(tidy_model44, 
          options = list(pageLength = 4), 
          caption = "Updated Regression Results") 
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}

prediction_data <- d_state_polls |>
  select(state, year, weeks_left, poll_date, poll_support, party) |>
  filter(month(as.Date(poll_date)) %in% c(9, 10), party == "DEM", year == 2024) |>
  group_by(year, state, month = month(as.Date(poll_date))) |>
  summarize(poll_support = round(weighted.mean(poll_support, weeks_left, na.rm = TRUE), 3), .groups = "drop") |>
  pivot_wider(names_from = month, 
              values_from = poll_support, 
              names_prefix = "month_") |>
  select(year,state, month_9, month_10) |>
  rename(September_Results = month_9, 
         October_Results = month_10) |>
  left_join(kaitlyn_dataset, by = c("state", "year")) |>
  mutate(across(everything(), ~ replace_na(., 0))) 

```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}
prediction_data

```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}

# Calculate predictions and confidence intervals
predictions <- predict(reg44, prediction_data, interval = "prediction")

# Convert predictions to a data frame and rename columns to avoid conflicts
predictions_df <- as.data.frame(predictions) |>
  rename(Prediction = fit, Lower_Bound = lwr, Upper_Bound = upr)

# Combine predictions with the original data
swing_state_predictions <- cbind(prediction_data, predictions_df)

# Add winner column based on the predicted vote share
swing_state_predictions <- swing_state_predictions |>
  mutate(Winner = ifelse(Prediction > 50, "Harris", "Trump")) |>
  filter(state %in% c("Arizona", "Georgia", "Michigan", "Nevada", "North Carolina", "Pennsylvania", "Wisconsin")) |>
  select(year, state, Prediction, Lower_Bound, Upper_Bound, Winner)
```

```{r, echo=FALSE, warning=FALSE, message=FALSE, include=FALSE}

swing_state_predictions
```

# Results: Do You Believe It??

Answer: I do not believe it. In this weeks prediction, you will see results for top swing states. Clearly, the lower and upper bounds of this prediction are *irregular* which I believe makes this prediction less than good science. I worked with my amazing classmate, Kaitlyn Vu, to try to correct these challenges, but was unable to do so. In any case, this is my prediction for the week!

```{r, echo=FALSE, warning=FALSE, message=FALSE}
#chat gpt
swing_state_predictions |>
  select(state, Prediction, Lower_Bound, Upper_Bound, Winner) |>
  gt() |>
  cols_label(
    state = "State",
    Prediction = "Prediction",
    Lower_Bound = "Lower Bound",
    Upper_Bound = "Upper Bound",
    Winner = "Winner"
  ) |>
  fmt_number(
    columns = c(Prediction, Lower_Bound, Upper_Bound),
    decimals = 2
  ) |>
  tab_style(
    style = cell_fill(color = "blue"),
    locations = cells_body(
      columns = Winner,
      rows = Winner == "Harris"
    )
  ) |>
  tab_style(
    style = cell_fill(color = "red"),
    locations = cells_body(
      columns = Winner,
      rows = Winner == "Trump"
    )
  ) |>
  tab_header(
    title = "Predicted Vote Share by State",
    subtitle = "Including Confidence Intervals and Winner Prediction"
  )
 
```

Citations - Assistance from Kaitlyn Vu with troubleshooting and code! - Chat GPT was used for the new table creation!
