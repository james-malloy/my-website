---
title: Flexdashboard in R
author: James Malloy
draft: true
date: '2022-03-18'
slug: []
categories:
  - dashboard
  - data visualization
tags:
  - dashboard
  - data visualization
---



A few months ago, a friend of mine told me about her desire to better track a virtual tutoring program that she manages. I asked her to let me make a dashboard for her, and she agreed. To make the dashboard, I used R and the Flexdashboard package and came up with this as (a replica of) the final product. Below, I'll outline the steps I took to come up with it.

## Step 1:  Access & load data

All the data is input and hosted on Google Sheets, so to access it I used the `googlesheets4` package along with a host of others. This was my first introduction to APIs (application programming interface), which allows two applications to talk to each other (in this case Google and R) and gain access to information that is otherwise private. 

It took me a while, but I was finally able to figure out the API stuff. For this post, I've created "fake" data in Google Sheets and made it publicly viewable. (This simplifies the process). However, I've commented out the code you'd need in real life to access your private Google Sheets data.



```r
library(googlesheets4) # access Google sheets data
library(flexdashboard) # dashboard package, great alternative to Shiny
library(shiny) # I still wanted to use some Shiny functionalities
library(DT) # nice html data tables
library(lubridate) # manipulating date data
library(plotly) # easy-to-code interactive plots
library(janitor) # cleaning names
library(tidyverse) # pipes, data wrangling, etc

# options(
#  gargle_oauth_cache = ".secrets",
#  gargle_oauth_email = TRUE)

# gs4_auth(scope = "https://www.googleapis.com/auth/drive")
# drive_auth(token = gs4_token())

gs4_deauth() # asking Google for permission to access data # gives R permission
             # publicly (not private) viewable Googlesheets only

gs_tutoring <- "1vyVNz2ClxDVcPr7oa1LTc0YyHwZ53DI_lBSvKtl3v8M" # Googlesheet data
```

## Step 2: Tidy the data

Data rarely comes in the form that you need it for proper analysis and visualizations. You often have to manipulate from a "wide" format into a "long" (aka "tidy") format. After your data is in the right format, you transform it to your heart's desire.

{{< panelset class="greetings" >}}
{{< panel name="Not tidy (How it's given) :thumbsdown:" >}}


```
## # A tibble: 28 x 60
##       id Status Orientation Day     Time     `Tutor Name` `Tutor Phone`
##    <int> <chr>  <chr>       <chr>   <chr>    <chr>        <chr>        
##  1     1 Active AB          Monday  4:30 PM  Tutor 1      <NA>         
##  2     2 Active ZR          Monday  4:45 PM  Tutor 2      <NA>         
##  3     3 Active DG          Monday  5:00 PM  Tutor 3      <NA>         
##  4     4 Active LJ          Monday  5:30 PM  Tutor 4      <NA>         
##  5     5 Active AB          Monday  5:30 PM  Tutor 5      <NA>         
##  6     6 Active ZR          Monday  5:30 PM  Tutor 6      <NA>         
##  7     7 Active DG          Monday  6:00 PM  Tutor 7      <NA>         
##  8     8 Active AB          Monday  6:00 PM  Tutor 8      <NA>         
##  9     9 Active ZR          Monday  6:00 PM  Tutor 9      <NA>         
## 10    10 Active DG          Tuesday 11:00 AM Tutor 10     <NA>         
## # ... with 18 more rows, and 53 more variables:
## #   `Tutor Unexcused Tardies` <chr>, `Tutor Unexcused Absences` <chr>,
## #   `Subject Tutored` <chr>, `Student Name` <chr>,
## #   `Student Unexcused Tardies` <chr>, `Student Unexcused Absences` <chr>,
## #   Cohort <chr>, Counselor <chr>, `Start Date` <date>,
## #   `Projected End Date` <date>, `Actual End Date` <date>, `2021-09-20` <chr>,
## #   `2021-09-27` <chr>, `2021-10-04` <chr>, `2021-10-11` <chr>, ...
```

{{< /panel >}}
{{< panel name="Tidy (How we want it) :thumbsup:" >}}


```r
df_attendance_long
```

```
## # A tibble: 1,008 x 27
##       id Status Orientation week_of    tutoring_date Day    Time    `Tutor Name`
##    <int> <chr>  <chr>       <date>     <date>        <chr>  <chr>   <chr>       
##  1     1 Active AB          2021-09-20 2021-09-20    Monday 4:30 PM Tutor 1     
##  2     1 Active AB          2021-09-27 2021-09-27    Monday 4:30 PM Tutor 1     
##  3     1 Active AB          2021-10-04 2021-10-04    Monday 4:30 PM Tutor 1     
##  4     1 Active AB          2021-10-11 2021-10-11    Monday 4:30 PM Tutor 1     
##  5     1 Active AB          2021-10-18 2021-10-18    Monday 4:30 PM Tutor 1     
##  6     1 Active AB          2021-10-25 2021-10-25    Monday 4:30 PM Tutor 1     
##  7     1 Active AB          2021-11-01 2021-11-01    Monday 4:30 PM Tutor 1     
##  8     1 Active AB          2021-11-08 2021-11-08    Monday 4:30 PM Tutor 1     
##  9     1 Active AB          2021-11-15 2021-11-15    Monday 4:30 PM Tutor 1     
## 10     1 Active AB          2021-11-22 2021-11-22    Monday 4:30 PM Tutor 1     
## # ... with 998 more rows, and 19 more variables: `Tutor Phone` <chr>,
## #   `Tutor Unexcused Tardies` <chr>, `Tutor Unexcused Absences` <chr>,
## #   `Subject Tutored` <chr>, `Student Name` <chr>,
## #   `Student Unexcused Tardies` <chr>, `Student Unexcused Absences` <chr>,
## #   Cohort <chr>, Counselor <chr>, `Start Date` <date>,
## #   `Projected End Date` <date>, `Actual End Date` <date>,
## #   `Total Sessions Missed` <dbl>, `Total Sessions  Held` <dbl>, ...
```

{{< /panel >}}
{{< panel name="Tidy (How we want it) :thumbsup:" >}}


```r
gs_attendance_col_types <-
  "ccccccccccccccDDDccccccccccccccccccccccccccccccccccccccccccccnnnn"

df_attendance <-
  read_sheet(gs_tutoring, 
             range = "A9:BM",
             n_max = 100,
             col_types = gs_attendance_col_types)%>% 
  select(-c("8/9", "8/16", "8/23", "8/30", "9/6", "9/13", "12/20", "12/27")) %>%
  mutate(id = row_number(), .before = "Status") %>%
  mutate(Day = case_when(
    Day == "MON" ~ "Monday",
    Day == "TUE" ~ "Tuesday",
    Day == "WED" ~ "Wednesday",
    Day == "TH" ~ "Thursday",
    Day == "F" ~ "Friday")) %>% 
  mutate(day_numeric = case_when(
    Day == "Monday" ~ 2,
    Day == "Tuesday" ~ 3,
    Day == "Wednesday" ~ 4,
    Day == "Thursday" ~ 5,
    Day == "Friday" ~ 6)) %>%
  mutate(`Attendance Percentage` = round(`Attendance Percentage` , digits = 2) * 100,
         `Attendance Proportion` = `Attendance Percentage` / 100) %>% 
  # What's a better way to do this? Regex?
  rename("2021-09-20" = "9/20",
         "2021-09-27" = "9/27",
         "2021-10-04" = "10/4",
         "2021-10-11" = "10/11",
         "2021-10-18" = "10/18",
         "2021-10-25" = "10/25",
         "2021-11-01" = "11/1",
         "2021-11-08" = "11/8",
         "2021-11-15" = "11/15",
         "2021-11-22" = "11/22",
         "2021-11-29" = "11/29",
         "2021-12-06" = "12/6",
         "2021-12-13" = "12/13",
         "2022-01-03" = "1/3",
         "2022-01-10" = "1/10",
         "2022-01-17" = "1/17",
         "2022-01-24" = "1/24",
         "2022-01-31" = "1/31",
         "2022-02-07" = "2/7",
         "2022-02-14" = "2/14",
         "2022-02-21" = "2/21",
         "2022-02-28" = "2/28",
         "2022-03-07" = "3/7",
         "2022-03-14" = "3/14",
         "2022-03-21" = "3/21",
         "2022-03-28" = "3/28",
         "2022-04-04" = "4/4",
         "2022-04-11" = "4/11",
         "2022-04-18" = "4/18",
         "2022-04-25" = "4/25",
         "2022-05-02" = "5/2",
         "2022-05-09" = "5/9",
         "2022-05-16" = "5/16",
         "2022-05-23" = "5/23",
         "2022-05-30" = "5/30",
         "2022-06-06" = "6/6")

df_attendance_long <-  df_attendance %>%
  pivot_longer(cols = matches("^[0-9]{4}-[0-9]{2}-[0-9]{2}$"),
               names_to = "week_of",
               values_to = "attendance_code") %>%
  mutate(week_of = ymd(week_of)) %>%
  mutate(attendance_code = case_when(attendance_code == "x" ~ "X", 
                                   TRUE ~ as.character(attendance_code))) %>% 
  mutate(tutoring_date = case_when(
    Day == "Monday" ~ as_date(week_of) + 0,
    Day == "Tuesday" ~ as_date(week_of) + 1,
    Day == "Wednesday" ~ as_date(week_of) + 2,
    Day == "Thursday" ~ as_date(week_of) + 3,
    Day == "Friday" ~ as_date(week_of) + 4), .before = "Day")%>% 
  relocate(week_of, .after = "Orientation")
```

{{< /panel >}}
{{< /panelset >}}

## Step 3: Visualize the data

Now that the data's in the proper format, it's time to visualize it. The Flexdashboard package has all sorts of neat functions like value boxes and gauges that are great for monitoring your metrics. If you want to visualize your data over time, the flexdashboard package integrates nicely with ggplot2 and plotly packages. The graph below shows attendance trends over time.

{{< panelset class="greetings" >}}
{{< panel name="Value Box :wave:" >}}


```r
n_total_sessions <- sum(df_attendance_long$attendance_code == "1",  
                      df_attendance_long$attendance_code == "2",
                      df_attendance_long$attendance_code == "3", na.rm = TRUE)

valueBox(
  n_total_sessions,
  icon = "fa-pencil",
  href = gs_tutoring)
```

## Step 4: Throw in some datatables

Another fave feature in my dashboards are datatables. Datatables 

And VOILA..a Flexdashboard! 

I'm technically cheating by omitting a final and arguably the most important step which is publishing your dashboard. Following the steps above will get you a dashboard, but it will accessible only to you. When creating a dashboard, nine  times out of ten you'll want it to be publicly accessible to other people. 

Flexdashboard can be pushed to the web using Shiny, which I must admit is no simple feat and honestly deserves its own post which I'll save for another day. But if anyone is interested in trying out Flexdashboard, feel free to reach out to me. I'm happy to help out if I can.
