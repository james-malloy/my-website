---
title: Visualizing Interrater Reliability
author: James Malloy
draft: true
date: '2022-03-05'
slug: []
categories: []
tags: []
editor_options: 
  chunk_output_type: console
---

<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/raphael/raphael-2.1.4.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/justgage/justgage.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/justgage/justgage.js"></script>
<script src="{{< blogdown/postref >}}index_files/gauge-binding/gauge.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery-3.6.0.min.js"></script>

In the realm of research, the term **reliability** refers to how consistently a method measures something. If the same result can be consistently achieved by using the same methods under the same circumstances, the measurement is considered reliable.

I’m currently working on a research study where participants have to construct written responses. Those written responses are then evaluated by my co-researcher and me, and then given a quality score of 3 (great), 2 (good), 1 (fair), or 0 (poor).

The graph below is a final summary our work and progress toward reaching reliability.

# Training 1 Round 1

The simplest way to think about reliability is % agreement, which is simply the percentage of times my co-researcher and I had perfect agreement. Percent agreement is a very straightforward concept. Unfortunately, it can also be challenging to reach because what one rater scores a 0, the other might score a 1, what one rater might score a 1, the other a 2, and so on and so on.

This proved to be true for my co-researcher and I as well. I calculate below our percent agreement for our 1st training session.

``` r
df_irr %>% summarize(mean(agree_round_1))# calculate percent agreement
```

    ## # A tibble: 1 x 1
    ##   `mean(agree_round_1)`
    ##                   <dbl>
    ## 1                 0.408

``` r
gauge(value = 40 , min = 0, max = 100,symbol = "%")
```

<div id="htmlwidget-1" style="width:672px;height:480px;" class="gauge html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"value":40,"min":0,"max":100,"customSectors":[{"lo":0,"hi":100,"color":"success"}],"symbol":"%","label":null,"humanFriendly":true,"humanFriendlyDecimal":1,"href":null},"evals":[],"jsHooks":[]}</script>

40%…YIKES! NOT GOOD! With percent agreement, you want to be in the 70-80% range, certainly no lower than 60%. What was the source of our disagreement? I explained part of it earlier that percent agreement means “perfect agreement.” In other words, you get no “bonus points” even if your scores are close to one another. Percent agreement could then be aptly changed to “perfect agreement.”

To consider the reality of the distribution of possible scores between scorers, researchers enlist another statistical tool call Cohen’s Kappa. What is Cohen’s Kappa?

Cohen’s kappa measures the agreement between two raters who each classify N items into C mutually exclusive categories.¹
A simple way to think this is that Cohen’s Kappa is a quantitative measure of reliability for two raters that are rating the same thing, corrected for how often that the raters may agree by chance.

https://towardsdatascience.com/cohens-kappa-9786ceceab58

Below I calculate cohen’s kappa for the same set of scores.

``` r
# to use the irr:cohen.kappa function, you must feed it a matrix with *just* the two scorers

df_round_1 <- # assign object to "df_round_1"
  df_irr %>%  # call original data frame
  select(rater_1_round_1, rater_2_round_1) %>% # select just the scores
  data.frame() # to use the cohen.kappa function you MUST feed it a data frame object

ck <- cohen.kappa(df_round_1) 

ggplot(tidy(ck), aes(estimate, type)) +
  geom_point() +
  geom_errorbarh(aes(xmin = conf.low, xmax = conf.high)) +
  labs(title = "Cohen's Kappa Round 1")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/round-1-1.png" width="672" />

``` r
ck %>% 
  tidy() %>% 
  kable(caption = "Cohen's Kappa Round 1", digits = 2)
```

<table>
<caption>
Table 1: Cohen’s Kappa Round 1
</caption>
<thead>
<tr>
<th style="text-align:left;">
type
</th>
<th style="text-align:right;">
estimate
</th>
<th style="text-align:right;">
conf.low
</th>
<th style="text-align:right;">
conf.high
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
unweighted
</td>
<td style="text-align:right;">
0.18
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:right;">
0.28
</td>
</tr>
<tr>
<td style="text-align:left;">
weighted
</td>
<td style="text-align:right;">
0.40
</td>
<td style="text-align:right;">
0.10
</td>
<td style="text-align:right;">
0.70
</td>
</tr>
</tbody>
</table>

Unfortunately, Cohen’s kappa doesn’t prove to be any better than the percent agreement and only leaves more questions. To get to the bottom of this, I decide to visualize our scores with a confusion matrix. T

``` r
cm_round_1 <- table(df_round_1) %>% as.data.frame()
# cm_round_1

ggplot(cm_round_1, aes(rater_1_round_1, rater_2_round_1, fill = Freq)) +
  geom_tile() +
  geom_text(aes(label = Freq)) +
  scale_fill_gradient(low="white", high="#009194") +
  theme_light() +
  labs(x = "Rater 1", y = "Rater 2")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/confusion-matrix-1.png" width="672" />

The confusion matrix reveals two problem areas:

-   when I (Rater 2) am scoring responses as 0 that my co-researcher is scoring as 1 and

-   when I (Rater 2) am scoring things as a 1 that my co-researcher is scoring as a 2.

By the looks of it, I’m a tough grader. To be fair, this study I’m working on is not my primary domain. I asked to be part of it to have some research experience under my belt. After pinpointing our problem areas, my co-researcher and I confer to discuss our different points of view. Eventually, we’re able to get our percent agreement and reliability to what you see below.

# Round 2

``` r
# Create matrix
df_round_2 <-
  df_irr %>% 
  select(rater_1_round_2, rater_2_round_2) %>% 
  data.frame()

irr::agree(df_round_2) # an alternative way to calculate % agreement
```

    ##  Percentage agreement (Tolerance=0)
    ## 
    ##  Subjects = 152 
    ##    Raters = 2 
    ##   %-agree = 88.2

``` r
cm_round_2 <- table(df_round_2) %>% as.data.frame()
# cm_round_2

ggplot(cm_round_2, aes(rater_1_round_2, rater_2_round_2, fill = Freq)) +
  geom_tile() +
  geom_text(aes(label = Freq)) +
  scale_fill_gradient(low="white", high="#009194") +
  theme_light() +
  labs(x = "Rater 1", y = "Rater 2")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/percent agreement-1.png" width="672" />

``` r
cohen.kappa(df_round_2) %>% 
  broom::tidy() %>% 
  kable(caption = "Cohen's Kappa Round 2", digits = 2)
```

<table>
<caption>
(\#tab:percent agreement)Cohen’s Kappa Round 2
</caption>
<thead>
<tr>
<th style="text-align:left;">
type
</th>
<th style="text-align:right;">
estimate
</th>
<th style="text-align:right;">
conf.low
</th>
<th style="text-align:right;">
conf.high
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
unweighted
</td>
<td style="text-align:right;">
0.81
</td>
<td style="text-align:right;">
0.73
</td>
<td style="text-align:right;">
0.89
</td>
</tr>
<tr>
<td style="text-align:left;">
weighted
</td>
<td style="text-align:right;">
0.87
</td>
<td style="text-align:right;">
0.87
</td>
<td style="text-align:right;">
0.87
</td>
</tr>
</tbody>
</table>

``` r
df_summary <- df_irr %>% 
  group_by(question) %>% 
  summarize(
    n = n(),
    agreement_round_1 = sum(agree_round_1 == 1)/n,
    agreement_round_2 = sum(agree_round_2 == 1)/n
    )


ggplot(df_summary, aes(x = question, y = agreement_round_1, color = agreement_round_1)) +
  geom_point(size = 5) +
  geom_point(color = "black", pch = 21, size = 5) +
  scale_color_gradient(low="white", high="#009194") +
  scale_y_continuous() +
  ylim(c(0,1)) +
  labs(y = "Percent Agreement",
       x = "Question") +
  theme_bw()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />
