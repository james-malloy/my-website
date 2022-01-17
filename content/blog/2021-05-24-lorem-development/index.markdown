---
title: "Lorem Arrested Development"
subtitle: "How to add panelsets in R Markdown posts."
excerpt: "Add tabbed sections with code and results."
date: 2021-05-24
author: "Alison Hill"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- evergreen
---

<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>

## Testing

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.6     v dplyr   1.0.7
    ## v tidyr   1.1.4     v stringr 1.4.0
    ## v readr   2.1.1     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(dplyr)
library(shiny)
library(palmerpenguins)
library(plotly)
```

    ## 
    ## Attaching package: 'plotly'

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     last_plot

    ## The following object is masked from 'package:stats':
    ## 
    ##     filter

    ## The following object is masked from 'package:graphics':
    ## 
    ##     layout

``` r
data(cars)

ggplotly(
ggplot(cars, aes(x = speed, y = dist)) +
  geom_point()
)
```

<div id="htmlwidget-1" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"data":[{"x":[4,4,7,7,8,9,10,10,10,11,11,12,12,12,12,13,13,13,13,14,14,14,14,15,15,15,16,16,17,17,17,18,18,18,18,19,19,19,20,20,20,20,20,22,23,24,24,24,24,25],"y":[2,10,4,22,16,10,18,26,34,17,28,14,20,24,28,26,34,34,46,26,36,60,80,20,26,54,32,40,32,40,50,42,56,76,84,36,46,68,32,48,52,56,64,66,54,70,92,93,120,85],"text":["speed:  4<br />dist:   2","speed:  4<br />dist:  10","speed:  7<br />dist:   4","speed:  7<br />dist:  22","speed:  8<br />dist:  16","speed:  9<br />dist:  10","speed: 10<br />dist:  18","speed: 10<br />dist:  26","speed: 10<br />dist:  34","speed: 11<br />dist:  17","speed: 11<br />dist:  28","speed: 12<br />dist:  14","speed: 12<br />dist:  20","speed: 12<br />dist:  24","speed: 12<br />dist:  28","speed: 13<br />dist:  26","speed: 13<br />dist:  34","speed: 13<br />dist:  34","speed: 13<br />dist:  46","speed: 14<br />dist:  26","speed: 14<br />dist:  36","speed: 14<br />dist:  60","speed: 14<br />dist:  80","speed: 15<br />dist:  20","speed: 15<br />dist:  26","speed: 15<br />dist:  54","speed: 16<br />dist:  32","speed: 16<br />dist:  40","speed: 17<br />dist:  32","speed: 17<br />dist:  40","speed: 17<br />dist:  50","speed: 18<br />dist:  42","speed: 18<br />dist:  56","speed: 18<br />dist:  76","speed: 18<br />dist:  84","speed: 19<br />dist:  36","speed: 19<br />dist:  46","speed: 19<br />dist:  68","speed: 20<br />dist:  32","speed: 20<br />dist:  48","speed: 20<br />dist:  52","speed: 20<br />dist:  56","speed: 20<br />dist:  64","speed: 22<br />dist:  66","speed: 23<br />dist:  54","speed: 24<br />dist:  70","speed: 24<br />dist:  92","speed: 24<br />dist:  93","speed: 24<br />dist: 120","speed: 25<br />dist:  85"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(0,0,0,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(0,0,0,1)"}},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":43.1050228310502},"plot_bgcolor":"rgba(235,235,235,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[2.95,26.05],"tickmode":"array","ticktext":["5","10","15","20","25"],"tickvals":[5,10,15,20,25],"categoryorder":"array","categoryarray":["5","10","15","20","25"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"speed","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-3.9,125.9],"tickmode":"array","ticktext":["0","25","50","75","100","125"],"tickvals":[0,25,50,75,100,125],"categoryorder":"array","categoryarray":["0","25","50","75","100","125"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"dist","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"4d845951f38":{"x":{},"y":{},"type":"scatter"}},"cur_data":"4d845951f38","visdat":{"4d845951f38":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

## But first, panelsets with R code chunks

{{&lt; panelset class=“greetings” &gt;}}
{{&lt; panel name=“Plot” &gt;}}

<img src="{{< blogdown/postref >}}index_files/figure-html/plot-1.png" width="672" />

{{&lt; /panel &gt;}}
{{&lt; panel name=“Code” &gt;}}

``` r
plot(pressure)
```

{{&lt; /panel &gt;}}
{{&lt; /panelset &gt;}}

## I’m half machine. I’m a monster.

It’s a hug, Michael. I’m hugging you. I’m half machine. I’m a monster. There’s only one man I’ve ever called a coward, and that’s Brian Doyle Murray. No, what I’m calling you is a television actor. Bad news. Andy Griffith turned us down. He didn’t like his trailer.

No, I did not kill Kitty. However, I am going to oblige and answer the nice officer’s questions because I am an honest man with no secrets to hide. Guy’s a pro. Really? **Did nothing cancel?** *Get me a vodka rocks.* And a piece of toast.

## No… but I’d like to be asked!

Oh, you’re gonna be in a coma, all right. Steve Holt! I hear the jury’s still out on science. No, I did not kill Kitty. However, I am going to oblige and answer the nice officer’s questions because I am an honest man with no secrets to hide.

1.  Really? Did nothing cancel?
2.  That’s what it said on ‘Ask Jeeves.’
3.  Get me a vodka rocks. And a piece of toast.

### That’s what it said on ‘Ask Jeeves.’

Did you enjoy your meal, Mom? You drank it fast enough. What’s Spanish for “I know you speak English?” Bad news. Andy Griffith turned us down. He didn’t like his trailer. Really? Did nothing cancel? I care deeply for nature.

-   Michael!
-   No! I was ashamed to be SEEN with you. I like being with you.
-   We just call it a sausage.

Well, what do you expect, mother? It’s called ‘taking advantage.’ It’s what gets you ahead in life. Now, when you do this without getting punched in the chest, you’ll have more fun. No, I did not kill Kitty. However, I am going to oblige and answer the nice officer’s questions because I am an honest man with no secrets to hide.

I’m half machine. I’m a monster. It’s a hug, Michael. I’m hugging you. Guy’s a pro. First place chick is hot, but has an attitude, doesn’t date magicians. He’ll want to use your yacht, and I don’t want this thing smelling like fish.

He’ll want to use your yacht, and I don’t want this thing smelling like fish. Now, when you do this without getting punched in the chest, you’ll have more fun. We just call it a sausage. Guy’s a pro. Bad news. Andy Griffith turned us down. He didn’t like his trailer.

There’s only one man I’ve ever called a coward, and that’s Brian Doyle Murray. No, what I’m calling you is a television actor. It’s called ‘taking advantage.’ It’s what gets you ahead in life. We just call it a sausage.

Michael! First place chick is hot, but has an attitude, doesn’t date magicians. I’ve opened a door here that I regret. Guy’s a pro.

Army had half a day. Michael! Now, when you do this without getting punched in the chest, you’ll have more fun. Well, what do you expect, mother? Now, when you do this without getting punched in the chest, you’ll have more fun.

But I bought a yearbook ad from you, doesn’t that mean anything anymore? Oh, you’re gonna be in a coma, all right. It’s a hug, Michael. I’m hugging you. I’ve opened a door here that I regret.

There’s only one man I’ve ever called a coward, and that’s Brian Doyle Murray. No, what I’m calling you is a television actor. That’s why you always leave a note! He’ll want to use your yacht, and I don’t want this thing smelling like fish.

I’ve opened a door here that I regret. Now, when you do this without getting punched in the chest, you’ll have more fun. I care deeply for nature. It’s called ‘taking advantage.’ It’s what gets you ahead in life.

It’s a hug, Michael. I’m hugging you. No… but I’d like to be asked! What’s Spanish for “I know you speak English?” It’s called ‘taking advantage.’ It’s what gets you ahead in life. It’s a hug, Michael. I’m hugging you.

I don’t understand the question, and I won’t respond to it. Really? Did nothing cancel? Did you enjoy your meal, Mom? You drank it fast enough. Bad news. Andy Griffith turned us down. He didn’t like his trailer.
