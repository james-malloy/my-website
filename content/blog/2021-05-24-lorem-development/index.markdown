---
title: "Lorem Arrested Development"
subtitle: "How to add panelsets in R Markdown posts."
excerpt: "Add tabbed sections with code and results."
date: 2021-05-24
author: "Alison Hill"
draft: true
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
ggplot(cars, aes(x = speed, y = dist, color = speed)) +
  geom_point()
)
```

<div id="htmlwidget-1" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"data":[{"x":[4,4,7,7,8,9,10,10,10,11,11,12,12,12,12,13,13,13,13,14,14,14,14,15,15,15,16,16,17,17,17,18,18,18,18,19,19,19,20,20,20,20,20,22,23,24,24,24,24,25],"y":[2,10,4,22,16,10,18,26,34,17,28,14,20,24,28,26,34,34,46,26,36,60,80,20,26,54,32,40,32,40,50,42,56,76,84,36,46,68,32,48,52,56,64,66,54,70,92,93,120,85],"text":["speed:  4<br />dist:   2<br />speed:  4","speed:  4<br />dist:  10<br />speed:  4","speed:  7<br />dist:   4<br />speed:  7","speed:  7<br />dist:  22<br />speed:  7","speed:  8<br />dist:  16<br />speed:  8","speed:  9<br />dist:  10<br />speed:  9","speed: 10<br />dist:  18<br />speed: 10","speed: 10<br />dist:  26<br />speed: 10","speed: 10<br />dist:  34<br />speed: 10","speed: 11<br />dist:  17<br />speed: 11","speed: 11<br />dist:  28<br />speed: 11","speed: 12<br />dist:  14<br />speed: 12","speed: 12<br />dist:  20<br />speed: 12","speed: 12<br />dist:  24<br />speed: 12","speed: 12<br />dist:  28<br />speed: 12","speed: 13<br />dist:  26<br />speed: 13","speed: 13<br />dist:  34<br />speed: 13","speed: 13<br />dist:  34<br />speed: 13","speed: 13<br />dist:  46<br />speed: 13","speed: 14<br />dist:  26<br />speed: 14","speed: 14<br />dist:  36<br />speed: 14","speed: 14<br />dist:  60<br />speed: 14","speed: 14<br />dist:  80<br />speed: 14","speed: 15<br />dist:  20<br />speed: 15","speed: 15<br />dist:  26<br />speed: 15","speed: 15<br />dist:  54<br />speed: 15","speed: 16<br />dist:  32<br />speed: 16","speed: 16<br />dist:  40<br />speed: 16","speed: 17<br />dist:  32<br />speed: 17","speed: 17<br />dist:  40<br />speed: 17","speed: 17<br />dist:  50<br />speed: 17","speed: 18<br />dist:  42<br />speed: 18","speed: 18<br />dist:  56<br />speed: 18","speed: 18<br />dist:  76<br />speed: 18","speed: 18<br />dist:  84<br />speed: 18","speed: 19<br />dist:  36<br />speed: 19","speed: 19<br />dist:  46<br />speed: 19","speed: 19<br />dist:  68<br />speed: 19","speed: 20<br />dist:  32<br />speed: 20","speed: 20<br />dist:  48<br />speed: 20","speed: 20<br />dist:  52<br />speed: 20","speed: 20<br />dist:  56<br />speed: 20","speed: 20<br />dist:  64<br />speed: 20","speed: 22<br />dist:  66<br />speed: 22","speed: 23<br />dist:  54<br />speed: 23","speed: 24<br />dist:  70<br />speed: 24","speed: 24<br />dist:  92<br />speed: 24","speed: 24<br />dist:  93<br />speed: 24","speed: 24<br />dist: 120<br />speed: 24","speed: 25<br />dist:  85<br />speed: 25"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":["rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(28,60,90,1)","rgba(28,60,90,1)","rgba(31,66,98,1)","rgba(34,72,106,1)","rgba(37,78,114,1)","rgba(37,78,114,1)","rgba(37,78,114,1)","rgba(40,84,122,1)","rgba(40,84,122,1)","rgba(43,90,131,1)","rgba(43,90,131,1)","rgba(43,90,131,1)","rgba(43,90,131,1)","rgba(46,97,139,1)","rgba(46,97,139,1)","rgba(46,97,139,1)","rgba(46,97,139,1)","rgba(49,103,148,1)","rgba(49,103,148,1)","rgba(49,103,148,1)","rgba(49,103,148,1)","rgba(52,109,156,1)","rgba(52,109,156,1)","rgba(52,109,156,1)","rgba(56,116,165,1)","rgba(56,116,165,1)","rgba(59,122,174,1)","rgba(59,122,174,1)","rgba(59,122,174,1)","rgba(62,129,183,1)","rgba(62,129,183,1)","rgba(62,129,183,1)","rgba(62,129,183,1)","rgba(66,136,192,1)","rgba(66,136,192,1)","rgba(66,136,192,1)","rgba(69,142,201,1)","rgba(69,142,201,1)","rgba(69,142,201,1)","rgba(69,142,201,1)","rgba(69,142,201,1)","rgba(76,156,219,1)","rgba(79,163,228,1)","rgba(83,170,238,1)","rgba(83,170,238,1)","rgba(83,170,238,1)","rgba(83,170,238,1)","rgba(86,177,247,1)"],"opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":["rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(28,60,90,1)","rgba(28,60,90,1)","rgba(31,66,98,1)","rgba(34,72,106,1)","rgba(37,78,114,1)","rgba(37,78,114,1)","rgba(37,78,114,1)","rgba(40,84,122,1)","rgba(40,84,122,1)","rgba(43,90,131,1)","rgba(43,90,131,1)","rgba(43,90,131,1)","rgba(43,90,131,1)","rgba(46,97,139,1)","rgba(46,97,139,1)","rgba(46,97,139,1)","rgba(46,97,139,1)","rgba(49,103,148,1)","rgba(49,103,148,1)","rgba(49,103,148,1)","rgba(49,103,148,1)","rgba(52,109,156,1)","rgba(52,109,156,1)","rgba(52,109,156,1)","rgba(56,116,165,1)","rgba(56,116,165,1)","rgba(59,122,174,1)","rgba(59,122,174,1)","rgba(59,122,174,1)","rgba(62,129,183,1)","rgba(62,129,183,1)","rgba(62,129,183,1)","rgba(62,129,183,1)","rgba(66,136,192,1)","rgba(66,136,192,1)","rgba(66,136,192,1)","rgba(69,142,201,1)","rgba(69,142,201,1)","rgba(69,142,201,1)","rgba(69,142,201,1)","rgba(69,142,201,1)","rgba(76,156,219,1)","rgba(79,163,228,1)","rgba(83,170,238,1)","rgba(83,170,238,1)","rgba(83,170,238,1)","rgba(83,170,238,1)","rgba(86,177,247,1)"]}},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[5],"y":[0],"name":"99_b9c3f54fa36de614f865bf7b8ef787a8","type":"scatter","mode":"markers","opacity":0,"hoverinfo":"skip","showlegend":false,"marker":{"color":[0,1],"colorscale":[[0,"#132B43"],[0.00334448160535118,"#132B44"],[0.00668896321070236,"#132C44"],[0.0100334448160535,"#142C45"],[0.0133779264214047,"#142D45"],[0.0167224080267559,"#142D46"],[0.020066889632107,"#142D46"],[0.0234113712374582,"#142E47"],[0.0267558528428093,"#152E47"],[0.0301003344481605,"#152F48"],[0.0334448160535117,"#152F48"],[0.0367892976588629,"#152F49"],[0.0401337792642141,"#153049"],[0.0434782608695652,"#16304A"],[0.0468227424749164,"#16304A"],[0.0501672240802676,"#16314B"],[0.0535117056856187,"#16314B"],[0.0568561872909699,"#16324C"],[0.0602006688963211,"#17324D"],[0.0635451505016722,"#17324D"],[0.0668896321070234,"#17334E"],[0.0702341137123746,"#17334E"],[0.0735785953177258,"#17344F"],[0.0769230769230769,"#18344F"],[0.0802675585284281,"#183450"],[0.0836120401337793,"#183550"],[0.0869565217391304,"#183551"],[0.0903010033444816,"#183651"],[0.0936454849498328,"#193652"],[0.0969899665551839,"#193652"],[0.100334448160535,"#193753"],[0.103678929765886,"#193754"],[0.107023411371237,"#193854"],[0.110367892976589,"#1A3855"],[0.11371237458194,"#1A3955"],[0.117056856187291,"#1A3956"],[0.120401337792642,"#1A3956"],[0.123745819397993,"#1A3A57"],[0.127090301003344,"#1B3A57"],[0.130434782608696,"#1B3B58"],[0.133779264214047,"#1B3B59"],[0.137123745819398,"#1B3B59"],[0.140468227424749,"#1C3C5A"],[0.1438127090301,"#1C3C5A"],[0.147157190635451,"#1C3D5B"],[0.150501672240803,"#1C3D5B"],[0.153846153846154,"#1C3D5C"],[0.157190635451505,"#1D3E5C"],[0.160535117056856,"#1D3E5D"],[0.163879598662207,"#1D3F5D"],[0.167224080267559,"#1D3F5E"],[0.17056856187291,"#1D3F5F"],[0.173913043478261,"#1E405F"],[0.177257525083612,"#1E4060"],[0.180602006688963,"#1E4160"],[0.183946488294314,"#1E4161"],[0.187290969899666,"#1E4261"],[0.190635451505017,"#1F4262"],[0.193979933110368,"#1F4263"],[0.197324414715719,"#1F4363"],[0.20066889632107,"#1F4364"],[0.204013377926421,"#1F4464"],[0.207357859531772,"#204465"],[0.210702341137124,"#204465"],[0.214046822742475,"#204566"],[0.217391304347826,"#204566"],[0.220735785953177,"#214667"],[0.224080267558528,"#214668"],[0.22742474916388,"#214768"],[0.230769230769231,"#214769"],[0.234113712374582,"#214769"],[0.237458193979933,"#22486A"],[0.240802675585284,"#22486A"],[0.244147157190635,"#22496B"],[0.247491638795987,"#22496C"],[0.250836120401338,"#224A6C"],[0.254180602006689,"#234A6D"],[0.25752508361204,"#234A6D"],[0.260869565217391,"#234B6E"],[0.264214046822743,"#234B6E"],[0.267558528428094,"#244C6F"],[0.270903010033445,"#244C70"],[0.274247491638796,"#244C70"],[0.277591973244147,"#244D71"],[0.280936454849498,"#244D71"],[0.284280936454849,"#254E72"],[0.287625418060201,"#254E72"],[0.290969899665552,"#254F73"],[0.294314381270903,"#254F74"],[0.297658862876254,"#254F74"],[0.301003344481605,"#265075"],[0.304347826086956,"#265075"],[0.307692307692308,"#265176"],[0.311036789297659,"#265176"],[0.31438127090301,"#275277"],[0.317725752508361,"#275278"],[0.321070234113712,"#275278"],[0.324414715719063,"#275379"],[0.327759197324415,"#275379"],[0.331103678929766,"#28547A"],[0.334448160535117,"#28547B"],[0.337792642140468,"#28557B"],[0.341137123745819,"#28557C"],[0.344481605351171,"#28567C"],[0.347826086956522,"#29567D"],[0.351170568561873,"#29567D"],[0.354515050167224,"#29577E"],[0.357859531772575,"#29577F"],[0.361204013377926,"#2A587F"],[0.364548494983278,"#2A5880"],[0.367892976588629,"#2A5980"],[0.37123745819398,"#2A5981"],[0.374581939799331,"#2A5982"],[0.377926421404682,"#2B5A82"],[0.381270903010033,"#2B5A83"],[0.384615384615385,"#2B5B83"],[0.387959866220736,"#2B5B84"],[0.391304347826087,"#2C5C85"],[0.394648829431438,"#2C5C85"],[0.397993311036789,"#2C5D86"],[0.40133779264214,"#2C5D86"],[0.404682274247492,"#2C5D87"],[0.408026755852843,"#2D5E87"],[0.411371237458194,"#2D5E88"],[0.414715719063545,"#2D5F89"],[0.418060200668896,"#2D5F89"],[0.421404682274247,"#2E608A"],[0.424749163879599,"#2E608A"],[0.42809364548495,"#2E618B"],[0.431438127090301,"#2E618C"],[0.434782608695652,"#2E618C"],[0.438127090301003,"#2F628D"],[0.441471571906354,"#2F628D"],[0.444816053511706,"#2F638E"],[0.448160535117057,"#2F638F"],[0.451505016722408,"#30648F"],[0.454849498327759,"#306490"],[0.45819397993311,"#306590"],[0.461538461538462,"#306591"],[0.464882943143813,"#306592"],[0.468227424749164,"#316692"],[0.471571906354515,"#316693"],[0.474916387959866,"#316793"],[0.478260869565217,"#316794"],[0.481605351170569,"#326895"],[0.48494983277592,"#326895"],[0.488294314381271,"#326996"],[0.491638795986622,"#326996"],[0.494983277591973,"#326997"],[0.498327759197324,"#336A98"],[0.501672240802676,"#336A98"],[0.505016722408027,"#336B99"],[0.508361204013378,"#336B99"],[0.511705685618729,"#346C9A"],[0.51505016722408,"#346C9B"],[0.518394648829431,"#346D9B"],[0.521739130434783,"#346D9C"],[0.525083612040134,"#346E9D"],[0.528428093645485,"#356E9D"],[0.531772575250836,"#356E9E"],[0.535117056856187,"#356F9E"],[0.538461538461538,"#356F9F"],[0.54180602006689,"#3670A0"],[0.545150501672241,"#3670A0"],[0.548494983277592,"#3671A1"],[0.551839464882943,"#3671A1"],[0.555183946488294,"#3772A2"],[0.558528428093645,"#3772A3"],[0.561872909698997,"#3773A3"],[0.565217391304348,"#3773A4"],[0.568561872909699,"#3773A4"],[0.57190635451505,"#3874A5"],[0.575250836120401,"#3874A6"],[0.578595317725752,"#3875A6"],[0.581939799331104,"#3875A7"],[0.585284280936455,"#3976A8"],[0.588628762541806,"#3976A8"],[0.591973244147157,"#3977A9"],[0.595317725752508,"#3977A9"],[0.59866220735786,"#3978AA"],[0.602006688963211,"#3A78AB"],[0.605351170568562,"#3A79AB"],[0.608695652173913,"#3A79AC"],[0.612040133779264,"#3A79AC"],[0.615384615384615,"#3B7AAD"],[0.618729096989967,"#3B7AAE"],[0.622073578595318,"#3B7BAE"],[0.625418060200669,"#3B7BAF"],[0.62876254180602,"#3C7CB0"],[0.632107023411371,"#3C7CB0"],[0.635451505016722,"#3C7DB1"],[0.638795986622073,"#3C7DB1"],[0.642140468227425,"#3C7EB2"],[0.645484949832776,"#3D7EB3"],[0.648829431438127,"#3D7FB3"],[0.652173913043478,"#3D7FB4"],[0.655518394648829,"#3D7FB5"],[0.65886287625418,"#3E80B5"],[0.662207357859532,"#3E80B6"],[0.665551839464883,"#3E81B6"],[0.668896321070234,"#3E81B7"],[0.672240802675585,"#3F82B8"],[0.675585284280936,"#3F82B8"],[0.678929765886288,"#3F83B9"],[0.682274247491639,"#3F83BA"],[0.68561872909699,"#4084BA"],[0.688963210702341,"#4084BB"],[0.692307692307692,"#4085BB"],[0.695652173913044,"#4085BC"],[0.698996655518395,"#4086BD"],[0.702341137123746,"#4186BD"],[0.705685618729097,"#4186BE"],[0.709030100334448,"#4187BF"],[0.712374581939799,"#4187BF"],[0.71571906354515,"#4288C0"],[0.719063545150502,"#4288C1"],[0.722408026755853,"#4289C1"],[0.725752508361204,"#4289C2"],[0.729096989966555,"#438AC2"],[0.732441471571906,"#438AC3"],[0.735785953177257,"#438BC4"],[0.739130434782609,"#438BC4"],[0.74247491638796,"#438CC5"],[0.745819397993311,"#448CC6"],[0.749163879598662,"#448DC6"],[0.752508361204013,"#448DC7"],[0.755852842809364,"#448EC8"],[0.759197324414716,"#458EC8"],[0.762541806020067,"#458FC9"],[0.765886287625418,"#458FC9"],[0.769230769230769,"#458FCA"],[0.77257525083612,"#4690CB"],[0.775919732441471,"#4690CB"],[0.779264214046823,"#4691CC"],[0.782608695652174,"#4691CD"],[0.785953177257525,"#4792CD"],[0.789297658862876,"#4792CE"],[0.792642140468227,"#4793CF"],[0.795986622073579,"#4793CF"],[0.79933110367893,"#4894D0"],[0.802675585284281,"#4894D0"],[0.806020066889632,"#4895D1"],[0.809364548494983,"#4895D2"],[0.812709030100334,"#4896D2"],[0.816053511705686,"#4996D3"],[0.819397993311037,"#4997D4"],[0.822742474916388,"#4997D4"],[0.826086956521739,"#4998D5"],[0.82943143812709,"#4A98D6"],[0.832775919732441,"#4A99D6"],[0.836120401337793,"#4A99D7"],[0.839464882943144,"#4A9AD8"],[0.842809364548495,"#4B9AD8"],[0.846153846153846,"#4B9BD9"],[0.849498327759197,"#4B9BDA"],[0.852842809364548,"#4B9BDA"],[0.8561872909699,"#4C9CDB"],[0.859531772575251,"#4C9CDB"],[0.862876254180602,"#4C9DDC"],[0.866220735785953,"#4C9DDD"],[0.869565217391304,"#4D9EDD"],[0.872909698996655,"#4D9EDE"],[0.876254180602007,"#4D9FDF"],[0.879598662207358,"#4D9FDF"],[0.882943143812709,"#4DA0E0"],[0.88628762541806,"#4EA0E1"],[0.889632107023411,"#4EA1E1"],[0.892976588628762,"#4EA1E2"],[0.896321070234114,"#4EA2E3"],[0.899665551839465,"#4FA2E3"],[0.903010033444816,"#4FA3E4"],[0.906354515050167,"#4FA3E5"],[0.909698996655518,"#4FA4E5"],[0.913043478260869,"#50A4E6"],[0.916387959866221,"#50A5E7"],[0.919732441471572,"#50A5E7"],[0.923076923076923,"#50A6E8"],[0.926421404682274,"#51A6E8"],[0.929765886287625,"#51A7E9"],[0.933110367892977,"#51A7EA"],[0.936454849498328,"#51A8EA"],[0.939799331103679,"#52A8EB"],[0.94314381270903,"#52A9EC"],[0.946488294314381,"#52A9EC"],[0.949832775919732,"#52AAED"],[0.953177257525084,"#53AAEE"],[0.956521739130435,"#53ABEE"],[0.959866220735786,"#53ABEF"],[0.963210702341137,"#53ACF0"],[0.966555183946488,"#54ACF0"],[0.969899665551839,"#54ADF1"],[0.973244147157191,"#54ADF2"],[0.976588628762542,"#54AEF2"],[0.979933110367893,"#55AEF3"],[0.983277591973244,"#55AFF4"],[0.986622073578595,"#55AFF4"],[0.989966555183946,"#55B0F5"],[0.993311036789298,"#56B0F6"],[0.996655518394649,"#56B1F6"],[1,"#56B1F7"]],"colorbar":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"thickness":23.04,"title":"speed","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"tickmode":"array","ticktext":["5","10","15","20","25"],"tickvals":[0.0476190476190476,0.285714285714286,0.523809523809524,0.761904761904762,1],"tickfont":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"ticklen":2,"len":0.5}},"xaxis":"x","yaxis":"y","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":43.1050228310502},"plot_bgcolor":"rgba(235,235,235,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[2.95,26.05],"tickmode":"array","ticktext":["5","10","15","20","25"],"tickvals":[5,10,15,20,25],"categoryorder":"array","categoryarray":["5","10","15","20","25"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"speed","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-3.9,125.9],"tickmode":"array","ticktext":["0","25","50","75","100","125"],"tickvals":[0,25,50,75,100,125],"categoryorder":"array","categoryarray":["0","25","50","75","100","125"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"dist","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"7ac9eb4c29":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"7ac9eb4c29","visdat":{"7ac9eb4c29":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

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

.panelset\[
.panel\[.panel-name\[R Code\]

``` r
# ... r code ...
```

\]
.panel\[.panel-name\[Plot\]
![](index_files/figure-html/oplot-1.png)\]
\]
\#\# I’m half machine. I’m a monster.

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
