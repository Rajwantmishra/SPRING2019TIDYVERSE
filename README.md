Part 1 : http://rpubs.com/Rajwantmishra/tidy

Part 2:  http://rpubs.com/Rajwantmishra/tidy2

Github Link :  https://github.com/Rajwantmishra/SPRING2019TIDYVERSE

For Part 2 request submitted  with pull request :  https://github.com/acatlin/SPRING2019TIDYVERSE/pull/5




``` r
All<- tidyverse::tidyverse_packages()

cli::boxx("Hello there! Let's Explore Tidyverse Package", padding = 1, float = "center")
```

    ## +--------------------------------------------------+
    ## |                                                  |
    ## |   Hello there! Let's Explore Tidyverse Package   |
    ## |                                                  |
    ## +--------------------------------------------------+

``` r
print(All)
```

    ##  [1] "broom"       "cli"         "crayon"      "dplyr"       "dbplyr"     
    ##  [6] "forcats"     "ggplot2"     "haven"       "hms"         "httr"       
    ## [11] "jsonlite"    "lubridate"   "magrittr"    "modelr"      "purrr"      
    ## [16] "readr"       "readxl\n(>=" "reprex"      "rlang"       "rstudioapi" 
    ## [21] "rvest"       "stringr"     "tibble"      "tidyr"       "xml2"       
    ## [26] "tidyverse"

Data Source
===========

from
<https://fivethirtyeight.com/features/the-worst-tweeter-in-politics-isnt-trump/>

<https://raw.githubusercontent.com/fivethirtyeight/data/master/twitter-ratio/BarackObama.csv>

readr : Read File
-----------------

There are many types of file and with readr package you can read your
data directly in R using readr’r method.

> > read\_csv() and read\_tsv() are special cases of the general
> > read\_delim(). They’re useful for reading the most common types of
> > flat file data, comma separated values and tab separated values,
> > respectively. read\_csv2() uses ; for the field separator and , for
> > the decimal point. This is common in some European countries.

### Read\_CSV

``` r
obama <- "https://raw.githubusercontent.com/fivethirtyeight/data/master/twitter-ratio/BarackObama.csv"

trump <- "https://github.com/fivethirtyeight/data/raw/master/twitter-ratio/realDonaldTrump.csv"

senators<- "https://github.com/fivethirtyeight/data/raw/master/twitter-ratio/senators.csv"


# Read in the dataset, we can user read_csv to read data from online or from local disk
D_obama <- read_csv(obama)
```

    ## Parsed with column specification:
    ## cols(
    ##   created_at = col_character(),
    ##   text = col_character(),
    ##   url = col_character(),
    ##   replies = col_double(),
    ##   retweets = col_double(),
    ##   favorites = col_double(),
    ##   user = col_character()
    ## )

``` r
D_trump <- read_csv(trump)
```

    ## Parsed with column specification:
    ## cols(
    ##   created_at = col_character(),
    ##   text = col_character(),
    ##   url = col_character(),
    ##   replies = col_double(),
    ##   retweets = col_double(),
    ##   favorites = col_double(),
    ##   user = col_character()
    ## )

``` r
D_senators <- read_csv(senators)
```

    ## Parsed with column specification:
    ## cols(
    ##   created_at = col_character(),
    ##   text = col_character(),
    ##   url = col_character(),
    ##   replies = col_double(),
    ##   retweets = col_double(),
    ##   favorites = col_double(),
    ##   user = col_character(),
    ##   bioguide_id = col_character(),
    ##   party = col_character(),
    ##   state = col_character()
    ## )

``` r
#I'll Work on only D_trump

# Let's take a look at what we have, We can use Glimse to see data with its data strcutre 
str(D_trump)
```

    ## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame': 3232 obs. of  7 variables:
    ##  $ created_at: chr  "10/23/17 12:30" "10/23/17 11:53" "10/23/17 11:42" "10/22/17 12:08" ...
    ##  $ text      : chr  "I had a very respectful conversation with the widow of Sgt. La David Johnson, and spoke his name from beginning"| __truncated__ "Two dozen NFL players continue to kneel during the National Anthem, showing total disrespect to our Flag &amp; "| __truncated__ "There will be NO change to your 401(k). This has always been a great and popular middle class tax break that wo"| __truncated__ "It is finally sinking through. 46% OF PEOPLE BELIEVE MAJOR NATIONAL NEWS ORGS FABRICATE STORIES ABOUT ME. FAKE "| __truncated__ ...
    ##  $ url       : chr  "https://twitter.com/realDonaldTrump/status/922440008971292672" "https://twitter.com/realDonaldTrump/status/922430688703451136" "https://twitter.com/realDonaldTrump/status/922428118685581313" "https://twitter.com/realDonaldTrump/status/922072236592435200" ...
    ##  $ replies   : num  46228 31419 9552 56238 32136 ...
    ##  $ retweets  : num  10243 14006 13719 25102 21573 ...
    ##  $ favorites : num  49468 62406 62662 112890 97145 ...
    ##  $ user      : chr  "realDonaldTrump" "realDonaldTrump" "realDonaldTrump" "realDonaldTrump" ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   created_at = col_character(),
    ##   ..   text = col_character(),
    ##   ..   url = col_character(),
    ##   ..   replies = col_double(),
    ##   ..   retweets = col_double(),
    ##   ..   favorites = col_double(),
    ##   ..   user = col_character()
    ##   .. )

``` r
head(D_trump)
```

    ## # A tibble: 6 x 7
    ##   created_at  text           url          replies retweets favorites user  
    ##   <chr>       <chr>          <chr>          <dbl>    <dbl>     <dbl> <chr> 
    ## 1 10/23/17 1~ I had a very ~ https://twi~   46228    10243     49468 realD~
    ## 2 10/23/17 1~ Two dozen NFL~ https://twi~   31419    14006     62406 realD~
    ## 3 10/23/17 1~ There will be~ https://twi~    9552    13719     62662 realD~
    ## 4 10/22/17 1~ It is finally~ https://twi~   56238    25102    112890 realD~
    ## 5 10/22/17 1~ Wacky Congres~ https://twi~   32136    21573     97145 realD~
    ## 6 10/22/17 1~ Doing intervi~ https://twi~   11153     7336     42415 realD~

### Set Column Name

``` r
#Lets add our Custom Column Name, there are many ways we can do it. 
# We can change the name after reading the data set. Or We can read data and apply our name as we read it.
# It looks like we need to skip five lines, which will remove the column names
# So lets create a vector with column names
names <- c("TweetDate", "Tweets", "TweetURL", "Count_Reply", "Count_Retweet", 
           "Count_Fav", "UserID")

# And then try reading the file again
Dn_trump <- read_csv(trump,skip=1, col_names = names)
```

    ## Parsed with column specification:
    ## cols(
    ##   TweetDate = col_character(),
    ##   Tweets = col_character(),
    ##   TweetURL = col_character(),
    ##   Count_Reply = col_double(),
    ##   Count_Retweet = col_double(),
    ##   Count_Fav = col_double(),
    ##   UserID = col_character()
    ## )

``` r
head(Dn_trump)
```

    ## # A tibble: 6 x 7
    ##   TweetDate  Tweets    TweetURL  Count_Reply Count_Retweet Count_Fav UserID
    ##   <chr>      <chr>     <chr>           <dbl>         <dbl>     <dbl> <chr> 
    ## 1 10/23/17 ~ I had a ~ https://~       46228         10243     49468 realD~
    ## 2 10/23/17 ~ Two doze~ https://~       31419         14006     62406 realD~
    ## 3 10/23/17 ~ There wi~ https://~        9552         13719     62662 realD~
    ## 4 10/22/17 ~ It is fi~ https://~       56238         25102    112890 realD~
    ## 5 10/22/17 ~ Wacky Co~ https://~       32136         21573     97145 realD~
    ## 6 10/22/17 ~ Doing in~ https://~       11153          7336     42415 realD~

### Read column by Type

Lets say you want to force some column datatype before you read it, You
can set type of column using `col_types` before you read in `read_csv`,
i.e. c = character, i = integer, n = number, d = double, l = logical, f
= factor, D = date, T = date time, t = time, ? = guess, or \_/- to skip
the column.

``` r
# Lets Try altername 
names(D_trump) <- names

# Read in given Type of data
Type <- 'cccdddc'
read_csv(trump,col_types = Type )
```

    ## # A tibble: 3,232 x 7
    ##    created_at  text           url         replies retweets favorites user  
    ##    <chr>       <chr>          <chr>         <dbl>    <dbl>     <dbl> <chr> 
    ##  1 10/23/17 1~ I had a very ~ https://tw~   46228    10243     49468 realD~
    ##  2 10/23/17 1~ Two dozen NFL~ https://tw~   31419    14006     62406 realD~
    ##  3 10/23/17 1~ There will be~ https://tw~    9552    13719     62662 realD~
    ##  4 10/22/17 1~ It is finally~ https://tw~   56238    25102    112890 realD~
    ##  5 10/22/17 1~ Wacky Congres~ https://tw~   32136    21573     97145 realD~
    ##  6 10/22/17 1~ Doing intervi~ https://tw~   11153     7336     42415 realD~
    ##  7 10/22/17 0~ ...2nd Amendm~ https://tw~   24267    16216     72208 realD~
    ##  8 10/22/17 0~ ...9 months t~ https://tw~   16223    15125     71597 realD~
    ##  9 10/21/17 2~ I agree getti~ https://tw~   13914    12682     64506 realD~
    ## 10 10/21/17 2~ "Just out, bu~ https://tw~   11117    16286     61853 realD~
    ## # ... with 3,222 more rows

``` r
#Chek data
head(D_trump)
```

    ## # A tibble: 6 x 7
    ##   TweetDate  Tweets    TweetURL  Count_Reply Count_Retweet Count_Fav UserID
    ##   <chr>      <chr>     <chr>           <dbl>         <dbl>     <dbl> <chr> 
    ## 1 10/23/17 ~ I had a ~ https://~       46228         10243     49468 realD~
    ## 2 10/23/17 ~ Two doze~ https://~       31419         14006     62406 realD~
    ## 3 10/23/17 ~ There wi~ https://~        9552         13719     62662 realD~
    ## 4 10/22/17 ~ It is fi~ https://~       56238         25102    112890 realD~
    ## 5 10/22/17 ~ Wacky Co~ https://~       32136         21573     97145 realD~
    ## 6 10/22/17 ~ Doing in~ https://~       11153          7336     42415 realD~

### Subset

``` r
# Lets say I want to Read Only 1st 2 Row of record
D_trump[1:2,]
```

    ## # A tibble: 2 x 7
    ##   TweetDate  Tweets    TweetURL  Count_Reply Count_Retweet Count_Fav UserID
    ##   <chr>      <chr>     <chr>           <dbl>         <dbl>     <dbl> <chr> 
    ## 1 10/23/17 ~ I had a ~ https://~       46228         10243     49468 realD~
    ## 2 10/23/17 ~ Two doze~ https://~       31419         14006     62406 realD~

``` r
#Read 1st TWO colum of data
D_trump[,1:2]
```

    ## # A tibble: 3,232 x 2
    ##    TweetDate     Tweets                                                    
    ##    <chr>         <chr>                                                     
    ##  1 10/23/17 12:~ I had a very respectful conversation with the widow of Sg~
    ##  2 10/23/17 11:~ Two dozen NFL players continue to kneel during the Nation~
    ##  3 10/23/17 11:~ There will be NO change to your 401(k). This has always b~
    ##  4 10/22/17 12:~ It is finally sinking through. 46% OF PEOPLE BELIEVE MAJO~
    ##  5 10/22/17 12:~ Wacky Congresswoman Wilson is the gift that keeps on givi~
    ##  6 10/22/17 11:~ Doing interview today with Maria Bartiromo at 10:00 A.M. ~
    ##  7 10/22/17 0:09 ...2nd Amendment, Strong Military, ISIS, historic VA impr~
    ##  8 10/22/17 0:02 ...9 months than this Administration. Over 50 Legislation~
    ##  9 10/21/17 23:~ I agree getting Tax Cuts approved  is important (we will ~
    ## 10 10/21/17 22:~ "Just out, but lightly reported: \"Fewest jobless claims ~
    ## # ... with 3,222 more rows

``` r
# Read 11 Row with 2nd and 3rd column only.
D_trump[11,2:3]
```

    ## # A tibble: 1 x 2
    ##   Tweets                                  TweetURL                         
    ##   <chr>                                   <chr>                            
    ## 1 Crooked Hillary Clinton spent hundreds~ https://twitter.com/realDonaldTr~

``` r
#Create a subset of Data with Count_Fav greater thsn 100k (100000)

D_trump_Fav_100k <- filter(D_trump,D_trump$Count_Fav > 100000)

head(D_trump_Fav_100k)
```

    ## # A tibble: 6 x 7
    ##   TweetDate  Tweets    TweetURL  Count_Reply Count_Retweet Count_Fav UserID
    ##   <chr>      <chr>     <chr>           <dbl>         <dbl>     <dbl> <chr> 
    ## 1 10/22/17 ~ It is fi~ https://~       56238         25102    112890 realD~
    ## 2 10/21/17 ~ Subject ~ https://~       38253         69410    205353 realD~
    ## 3 10/20/17 ~ "Just ou~ https://~       52558         29383    106684 realD~
    ## 4 10/19/17 ~ Uranium ~ https://~       26991         39948    117721 realD~
    ## 5 10/18/17 ~ The NFL ~ https://~       50773         24359    100626 realD~
    ## 6 10/17/17 ~ BORDER W~ https://~       25000         30876    103617 realD~

lubridate : Working with date
-----------------------------

Want to read day, month, date, weekday, hours etc information from date
time value. Lubridate gives handy function to do it: \#\#\# Read Date

``` r
#Lets Work With Date
# Read 1 Record of date 
D_trump$TweetDate[1]
```

    ## [1] "10/23/17 12:30"

``` r
#Lets Split Date and Time 
date_string <- str_split(D_trump$TweetDate[1]," ",n=2,simplify = TRUE)
date_string
```

    ##      [,1]       [,2]   
    ## [1,] "10/23/17" "12:30"

``` r
data_date <- date_string[1,1]
data_date
```

    ## [1] "10/23/17"

``` r
data_time <- date_string[1,2]
data_time
```

    ## [1] "12:30"

``` r
new_date <- paste0(D_trump$TweetDate[1],":00")
new_date
```

    ## [1] "10/23/17 12:30:00"

``` r
lub_date <- mdy_hms(new_date)
lub_date
```

    ## [1] "2017-10-23 12:30:00 UTC"

``` r
# set Time Zone of the Date
tz(lub_date) <- "America/New_York"
```

### Month

``` r
#TO get Month 
month(lub_date) # Will Return only Number 
```

    ## [1] 10

``` r
month(lub_date,label = TRUE) # Will return Name of the month.
```

    ## [1] Oct
    ## 12 Levels: Jan < Feb < Mar < Apr < May < Jun < Jul < Aug < Sep < ... < Dec

### Days

``` r
day(lub_date) # Which Days in MOnth
```

    ## [1] 23

``` r
days_in_month(lub_date) # How many months are in this Month
```

    ## Oct 
    ##  31

### Weekday

``` r
# We can also extract some derived values such as the weekday
wday(lub_date)
```

    ## [1] 2

``` r
wday(lub_date, label = TRUE)
```

    ## [1] Mon
    ## Levels: Sun < Mon < Tue < Wed < Thu < Fri < Sat

### Day of the year

``` r
# or day of the year
yday(lub_date)
```

    ## [1] 296

### Change Timezone

``` r
# Changes time
with_tz(lub_date)
```

    ## [1] "2017-10-23 12:30:00 EDT"

``` r
with_tz(lub_date, "America/Chicago")
```

    ## [1] "2017-10-23 11:30:00 CDT"

``` r
with_tz(lub_date, "America/Los_Angeles")
```

    ## [1] "2017-10-23 09:30:00 PDT"

### Current Time

``` r
now()
```

    ## [1] "2019-04-20 00:52:16 EDT"

``` r
tz(now())
```

    ## [1] ""

### Date in Interval

%within%

Tests Whether A Date Or Interval Falls Within An Interval recycled
according to standard R rules. If b is a list of intervals, a is checked
if it falls within any of the intervals in b. If a is an interval, both
its start and end dates must fall within b to return TRUE.

``` r
## recycling
dates <- ymd(c("2014-12-20", "2014-12-30", "2015-01-01", "2015-01-03"))
blackouts<- c(interval(ymd("2014-12-30"), ymd("2014-12-31")),
              interval(ymd("2014-12-30"), ymd("2015-01-03")))
dates %within% blackouts
```

    ## [1] FALSE  TRUE FALSE  TRUE

``` r
# lets Put all the date vlaues together 
D_trump$newDate <- mdy_hms(paste0(D_trump$TweetDate,":00"))
  tz(D_trump$newDate)<- "America/New_York"
 D_trump$month <- month(D_trump$newDate ,label = TRUE)
 D_trump$wday <- wday(D_trump$newDate, label = TRUE)
```

ggplot2 package
---------------

### Subset of Data

``` r
# create a subset of data with only valid data value 
 newTestDate <- D_trump[,c("newDate","month","wday","Count_Retweet","Count_Reply")]
```

### Bar graph

``` r
# create the Base ggplot2 code to initialize it
g_base <- ggplot(newTestDate,mapping = aes(x=wday , y= Count_Reply, fill=wday))
g_base + geom_col()
```

![](TidyVerse_files/figure-markdown_github/unnamed-chunk-21-1.png)

### Using scatterplot

``` r
ggplot(newTestDate,mapping = aes(x=newDate , y= Count_Reply, color=wday)) + geom_point()
```

![](TidyVerse_files/figure-markdown_github/unnamed-chunk-22-1.png)

### Using facet\_wrap

Using wrap function

``` r
# Use the code.
g_base + geom_col() + facet_wrap(~month(D_trump$newDate)) 
```

![](TidyVerse_files/figure-markdown_github/unnamed-chunk-23-1.png)

### Using Theme

``` r
  ggplot(newTestDate)+
  geom_density(mapping=aes(x=Count_Reply ),alpha=.2, fill="#FF6666")+facet_wrap(~month(newTestDate$newDate)) +
    ggtitle("Reply by Month") +
  ylab("Count Reply") + xlab("Month") +
   theme(legend.position="top")
```

![](TidyVerse_files/figure-markdown_github/unnamed-chunk-24-1.png)

``` r
 ggplot( fct_count(newTestDate$month),mapping = aes(x= f, y=n )) + geom_col() 
```

![](TidyVerse_files/figure-markdown_github/unnamed-chunk-24-2.png)

### Using Density

``` r
  ggplot( fct_count(newTestDate$month))+
   geom_density(mapping=aes(x=n ),alpha=.2, fill="#FF6666") 
```

![](TidyVerse_files/figure-markdown_github/unnamed-chunk-25-1.png)

### Using Geom Smooth

``` r
  filter(newTestDate,wday == "Sun") %>%
  ggplot(mapping = aes(x=date(newDate) , y=Count_Retweet , color=wday)) + 
    geom_smooth(alpha=.2,span=.5, method = 'auto',  stat = "smooth") 
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](TidyVerse_files/figure-markdown_github/unnamed-chunk-26-1.png)

-   Using smooth with method

``` r
   filter(newTestDate,wday %in% c("Sat","Sun","Mon","Tue")) %>%
  ggplot(mapping = aes(x=date(newDate) , y=Count_Retweet , color=wday)) +
  geom_smooth(method = lm, se = FALSE)
```

![](TidyVerse_files/figure-markdown_github/unnamed-chunk-27-1.png)

dplyr : Working with Group by
-----------------------------

### Checking Group By

``` r
  print(newTestDate)
```

    ## # A tibble: 3,232 x 5
    ##    newDate             month wday  Count_Retweet Count_Reply
    ##    <dttm>              <ord> <ord>         <dbl>       <dbl>
    ##  1 2017-10-23 12:30:00 Oct   Mon           10243       46228
    ##  2 2017-10-23 11:53:00 Oct   Mon           14006       31419
    ##  3 2017-10-23 11:42:00 Oct   Mon           13719        9552
    ##  4 2017-10-22 12:08:00 Oct   Sun           25102       56238
    ##  5 2017-10-22 12:02:00 Oct   Sun           21573       32136
    ##  6 2017-10-22 11:50:00 Oct   Sun            7336       11153
    ##  7 2017-10-22 00:09:00 Oct   Sun           16216       24267
    ##  8 2017-10-22 00:02:00 Oct   Sun           15125       16223
    ##  9 2017-10-21 23:57:00 Oct   Sat           12682       13914
    ## 10 2017-10-21 22:51:00 Oct   Sat           16286       11117
    ## # ... with 3,222 more rows

``` r
  # I want to list all Tweets by Month and day
  # We can user group_by to group our data. 
  # Note: Group_by has no impact on data untill we use with some other function to run aggregation on it. Like summarise 
  group_by(newTestDate,month,wday)%>%summarise(Tweetcount  = n()) 
```

    ## # A tibble: 84 x 3
    ## # Groups:   month [12]
    ##    month wday  Tweetcount
    ##    <ord> <ord>      <int>
    ##  1 Jan   Sun           31
    ##  2 Jan   Mon           26
    ##  3 Jan   Tue           34
    ##  4 Jan   Wed           33
    ##  5 Jan   Thu           30
    ##  6 Jan   Fri           40
    ##  7 Jan   Sat           18
    ##  8 Feb   Sun           19
    ##  9 Feb   Mon           13
    ## 10 Feb   Tue           14
    ## # ... with 74 more rows

``` r
  #Lets validate your result with table 
    table(newTestDate$month,newTestDate$wday)
```

    ##      
    ##       Sun Mon Tue Wed Thu Fri Sat
    ##   Jan  31  26  34  33  30  40  18
    ##   Feb  19  13  14  28  23  23  27
    ##   Mar   6  16  24  21  27  35  14
    ##   Apr  22  25  21  20  22  13  27
    ##   May  18  20  21  25  23  26  13
    ##   Jun  15  35  40  27  38  38  15
    ##   Jul  28  37  37  35  21  33  51
    ##   Aug  27  42  39  54  56  65  46
    ##   Sep  68  46 117  82  98  91  91
    ##   Oct  85 130  81 135 159  55  88
    ##   Nov  35  17  55  34  15  21  15
    ##   Dec  20  15  22  15  20  17  28

``` r
    group_by(newTestDate,month,wday)%>%summarise(Tweetcount  = sum(Count_Retweet))
```

    ## # A tibble: 84 x 3
    ## # Groups:   month [12]
    ##    month wday  Tweetcount
    ##    <ord> <ord>      <dbl>
    ##  1 Jan   Sun       719156
    ##  2 Jan   Mon       592222
    ##  3 Jan   Tue       562292
    ##  4 Jan   Wed       644696
    ##  5 Jan   Thu       573091
    ##  6 Jan   Fri       897298
    ##  7 Jan   Sat       378400
    ##  8 Feb   Sun       403334
    ##  9 Feb   Mon       326946
    ## 10 Feb   Tue       283436
    ## # ... with 74 more rows

``` r
    ungroup(newTestDate)
```

    ## # A tibble: 3,232 x 5
    ##    newDate             month wday  Count_Retweet Count_Reply
    ##    <dttm>              <ord> <ord>         <dbl>       <dbl>
    ##  1 2017-10-23 12:30:00 Oct   Mon           10243       46228
    ##  2 2017-10-23 11:53:00 Oct   Mon           14006       31419
    ##  3 2017-10-23 11:42:00 Oct   Mon           13719        9552
    ##  4 2017-10-22 12:08:00 Oct   Sun           25102       56238
    ##  5 2017-10-22 12:02:00 Oct   Sun           21573       32136
    ##  6 2017-10-22 11:50:00 Oct   Sun            7336       11153
    ##  7 2017-10-22 00:09:00 Oct   Sun           16216       24267
    ##  8 2017-10-22 00:02:00 Oct   Sun           15125       16223
    ##  9 2017-10-21 23:57:00 Oct   Sat           12682       13914
    ## 10 2017-10-21 22:51:00 Oct   Sat           16286       11117
    ## # ... with 3,222 more rows

``` r
    # Lets take a long route to get the same data for our validation.
    # I'll Create a subset of data for MOnth = Jan and Weekday = Sun and then will do sum of count_retweet. 
    checkWeekDay <- filter(newTestDate,newTestDate$month=="Jan" & newTestDate$wday =="Sun")
    sum(checkWeekDay$Count_Retweet)
```

    ## [1] 719156

``` r
    # Wow, our data from last group_by output matches.
```

### Working with filter

``` r
#---------------------------------

# filter()
# 

# List all the Tweet whcih has more than 100 reply 
filter(D_trump,D_trump$Count_Reply > 100)
```

    ## # A tibble: 3,232 x 10
    ##    TweetDate Tweets TweetURL Count_Reply Count_Retweet Count_Fav UserID
    ##    <chr>     <chr>  <chr>          <dbl>         <dbl>     <dbl> <chr> 
    ##  1 10/23/17~ I had~ https:/~       46228         10243     49468 realD~
    ##  2 10/23/17~ Two d~ https:/~       31419         14006     62406 realD~
    ##  3 10/23/17~ There~ https:/~        9552         13719     62662 realD~
    ##  4 10/22/17~ It is~ https:/~       56238         25102    112890 realD~
    ##  5 10/22/17~ Wacky~ https:/~       32136         21573     97145 realD~
    ##  6 10/22/17~ Doing~ https:/~       11153          7336     42415 realD~
    ##  7 10/22/17~ ...2n~ https:/~       24267         16216     72208 realD~
    ##  8 10/22/17~ ...9 ~ https:/~       16223         15125     71597 realD~
    ##  9 10/21/17~ I agr~ https:/~       13914         12682     64506 realD~
    ## 10 10/21/17~ "Just~ https:/~       11117         16286     61853 realD~
    ## # ... with 3,222 more rows, and 3 more variables: newDate <dttm>,
    ## #   month <ord>, wday <ord>

stringr package
---------------

### Find word

Find word starting with something

``` r
# Using Stringr lets say I want to know all the Tweets that were Retweeted. 
filter(D_trump,str_detect(D_trump$Tweets,"^RT")) 
```

    ## # A tibble: 354 x 10
    ##    TweetDate Tweets TweetURL Count_Reply Count_Retweet Count_Fav UserID
    ##    <chr>     <chr>  <chr>          <dbl>         <dbl>     <dbl> <chr> 
    ##  1 10/21/17~ RT @I~ https:/~        2555          5355     20354 realD~
    ##  2 10/19/17~ "RT @~ https:/~       22017          8273     35846 realD~
    ##  3 10/17/17~ "RT @~ https:/~        4058          7773     27962 realD~
    ##  4 10/16/17~ "RT @~ https:/~        5225          5575     25420 realD~
    ##  5 10/16/17~ "RT @~ https:/~        6502          5849     25588 realD~
    ##  6 10/14/17~ "RT @~ https:/~        6103          4504     24172 realD~
    ##  7 10/14/17~ "RT @~ https:/~        6096          5840     33380 realD~
    ##  8 10/14/17~ "RT @~ https:/~        6195          7975     40910 realD~
    ##  9 10/14/17~ "RT @~ https:/~       10648         11415     48761 realD~
    ## 10 10/14/17~ "RT @~ https:/~        3701          6951     22148 realD~
    ## # ... with 344 more rows, and 3 more variables: newDate <dttm>,
    ## #   month <ord>, wday <ord>

### Find exact

``` r
# Check how many Time Border is as an issue got mention in tweet. 
filter(D_trump,str_detect(D_trump$Tweets," border|Border|BORDER")) 
```

    ## # A tibble: 55 x 10
    ##    TweetDate Tweets TweetURL Count_Reply Count_Retweet Count_Fav UserID
    ##    <chr>     <chr>  <chr>          <dbl>         <dbl>     <dbl> <chr> 
    ##  1 10/22/17~ ...9 ~ https:/~       16223         15125     71597 realD~
    ##  2 10/17/17~ BORDE~ https:/~       25000         30876    103617 realD~
    ##  3 10/11/17~ The D~ https:/~       19442         19443     84611 realD~
    ##  4 10/10/17~ The p~ https:/~       21637         22304     87047 realD~
    ##  5 9/20/17 ~ "Alab~ https:/~        7657          7458     44134 realD~
    ##  6 9/14/17 ~ ...Th~ https:/~       19227         10890     53442 realD~
    ##  7 9/14/17 ~ No de~ https:/~       12738         17414     64733 realD~
    ##  8 9/10/17 ~ "RT @~ https:/~        1117          5226     23621 realD~
    ##  9 8/25/17 ~ Few, ~ https:/~       34911         15900     72957 realD~
    ## 10 8/24/17 ~ On Tu~ https:/~        6557         12598     57231 realD~
    ## # ... with 45 more rows, and 3 more variables: newDate <dttm>,
    ## #   month <ord>, wday <ord>

### find all the Pattern

``` r
# We can use Filter to create SUBSET of data based on need
filter(D_trump,str_detect(D_trump$Tweets,"@[[:alnum:]]+")) 
```

    ## # A tibble: 917 x 10
    ##    TweetDate Tweets TweetURL Count_Reply Count_Retweet Count_Fav UserID
    ##    <chr>     <chr>  <chr>          <dbl>         <dbl>     <dbl> <chr> 
    ##  1 10/22/17~ Doing~ https:/~       11153          7336     42415 realD~
    ##  2 10/21/17~ "Just~ https:/~       11117         16286     61853 realD~
    ##  3 10/21/17~ RT @I~ https:/~        2555          5355     20354 realD~
    ##  4 10/20/17~ "Toda~ https:/~        4644          6894     34922 realD~
    ##  5 10/20/17~ Thank~ https:/~        9395         12757     47309 realD~
    ##  6 10/20/17~ Great~ https:/~        9658         12767     53372 realD~
    ##  7 10/20/17~ Big r~ https:/~       10478          9778     50938 realD~
    ##  8 10/19/17~ "It w~ https:/~        9335         10865     48875 realD~
    ##  9 10/19/17~ "RT @~ https:/~       22017          8273     35846 realD~
    ## 10 10/19/17~ ".@fo~ https:/~       25491         23359     71378 realD~
    ## # ... with 907 more rows, and 3 more variables: newDate <dttm>,
    ## #   month <ord>, wday <ord>

``` r
# We can also work on data column and store result for further processing 
At_Tweet<- str_extract_all(D_trump$Tweets,"@[[:alnum:]]+",simplify = TRUE)

tail(At_Tweet,15)
```

    ##         [,1]       [,2]     [,3]               [,4] [,5] [,6] [,7]
    ## [3218,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3219,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3220,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3221,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3222,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3223,] "@CNN"     ""       ""                 ""   ""   ""   ""  
    ## [3224,] "@Trump"   "@Nigel" "@realDonaldTrump" ""   ""   ""   ""  
    ## [3225,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3226,] "@Mike"    ""       ""                 ""   ""   ""   ""  
    ## [3227,] "@FoxNews" ""       ""                 ""   ""   ""   ""  
    ## [3228,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3229,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3230,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3231,] ""         ""       ""                 ""   ""   ""   ""  
    ## [3232,] ""         ""       ""                 ""   ""   ""   ""

dplyr : Working with Join
-------------------------

-   full\_join
-   inner\_join
-   anti\_join
-   left\_join
-   right\_join
-   nest\_join
-   semi\_join

### Data

``` r
#----------------------JOIN
table1 <- D_trump[5:20,c("TweetURL","TweetDate")]
table2 <- D_trump[1:15,c("TweetURL","Tweets")]

glimpse(table1)
```

    ## Observations: 16
    ## Variables: 2
    ## $ TweetURL  <chr> "https://twitter.com/realDonaldTrump/status/92207065...
    ## $ TweetDate <chr> "10/22/17 12:02", "10/22/17 11:50", "10/22/17 0:09",...

``` r
glimpse(table2)
```

    ## Observations: 15
    ## Variables: 2
    ## $ TweetURL <chr> "https://twitter.com/realDonaldTrump/status/922440008...
    ## $ Tweets   <chr> "I had a very respectful conversation with the widow ...

### Full\_join

``` r
# URL in Unique for each Tweet
table_Full <- table1 %>% dplyr::full_join(table2, by =c("TweetURL" = "TweetURL"))
glimpse(table_Full)
```

    ## Observations: 20
    ## Variables: 3
    ## $ TweetURL  <chr> "https://twitter.com/realDonaldTrump/status/92207065...
    ## $ TweetDate <chr> "10/22/17 12:02", "10/22/17 11:50", "10/22/17 0:09",...
    ## $ Tweets    <chr> "Wacky Congresswoman Wilson is the gift that keeps o...

``` r
# Note how all the Data set got clubbed here , we can see NA for Text for some Entry and NA for Created_at for some entry
table_Full
```

    ## # A tibble: 20 x 3
    ##    TweetURL                      TweetDate  Tweets                         
    ##    <chr>                         <chr>      <chr>                          
    ##  1 https://twitter.com/realDona~ 10/22/17 ~ Wacky Congresswoman Wilson is ~
    ##  2 https://twitter.com/realDona~ 10/22/17 ~ Doing interview today with Mar~
    ##  3 https://twitter.com/realDona~ 10/22/17 ~ ...2nd Amendment, Strong Milit~
    ##  4 https://twitter.com/realDona~ 10/22/17 ~ ...9 months than this Administ~
    ##  5 https://twitter.com/realDona~ 10/21/17 ~ I agree getting Tax Cuts appro~
    ##  6 https://twitter.com/realDona~ 10/21/17 ~ "Just out, but lightly reporte~
    ##  7 https://twitter.com/realDona~ 10/21/17 ~ Crooked Hillary Clinton spent ~
    ##  8 https://twitter.com/realDona~ 10/21/17 ~ "Keep hearing about \"tiny\" a~
    ##  9 https://twitter.com/realDona~ 10/21/17 ~ "Officials behind the now disc~
    ## 10 https://twitter.com/realDona~ 10/21/17 ~ "\x89\xdb\xcfTrump hails liber~
    ## 11 https://twitter.com/realDona~ 10/21/17 ~ Stock Market hits another all ~
    ## 12 https://twitter.com/realDona~ 10/21/17 ~ <NA>                           
    ## 13 https://twitter.com/realDona~ 10/21/17 ~ <NA>                           
    ## 14 https://twitter.com/realDona~ 10/21/17 ~ <NA>                           
    ## 15 https://twitter.com/realDona~ 10/21/17 ~ <NA>                           
    ## 16 https://twitter.com/realDona~ 10/21/17 ~ <NA>                           
    ## 17 https://twitter.com/realDona~ <NA>       I had a very respectful conver~
    ## 18 https://twitter.com/realDona~ <NA>       Two dozen NFL players continue~
    ## 19 https://twitter.com/realDona~ <NA>       There will be NO change to you~
    ## 20 https://twitter.com/realDona~ <NA>       It is finally sinking through.~

### inner\_join

``` r
#Inner Join 
table_Inner <- inner_join(table1,table2, by =c("TweetURL" = "TweetURL"))
```

``` r
# Here table_Inner would have all the data that is common in table1 and Table2
table_Inner
```

    ## # A tibble: 11 x 3
    ##    TweetURL                      TweetDate  Tweets                         
    ##    <chr>                         <chr>      <chr>                          
    ##  1 https://twitter.com/realDona~ 10/22/17 ~ Wacky Congresswoman Wilson is ~
    ##  2 https://twitter.com/realDona~ 10/22/17 ~ Doing interview today with Mar~
    ##  3 https://twitter.com/realDona~ 10/22/17 ~ ...2nd Amendment, Strong Milit~
    ##  4 https://twitter.com/realDona~ 10/22/17 ~ ...9 months than this Administ~
    ##  5 https://twitter.com/realDona~ 10/21/17 ~ I agree getting Tax Cuts appro~
    ##  6 https://twitter.com/realDona~ 10/21/17 ~ "Just out, but lightly reporte~
    ##  7 https://twitter.com/realDona~ 10/21/17 ~ Crooked Hillary Clinton spent ~
    ##  8 https://twitter.com/realDona~ 10/21/17 ~ "Keep hearing about \"tiny\" a~
    ##  9 https://twitter.com/realDona~ 10/21/17 ~ "Officials behind the now disc~
    ## 10 https://twitter.com/realDona~ 10/21/17 ~ "\x89\xdb\xcfTrump hails liber~
    ## 11 https://twitter.com/realDona~ 10/21/17 ~ Stock Market hits another all ~

### anti\_join

``` r
# if you want to list all the data from Table1, which is not in table2 we can use anti_join 
table_Anti <- dplyr::anti_join(table1,table2, by =c("TweetURL" = "TweetURL"))

table_Anti
```

    ## # A tibble: 5 x 2
    ##   TweetURL                                                    TweetDate    
    ##   <chr>                                                       <chr>        
    ## 1 https://twitter.com/realDonaldTrump/status/921724821939130~ 10/21/17 13:~
    ## 2 https://twitter.com/realDonaldTrump/status/921723302481145~ 10/21/17 13:~
    ## 3 https://twitter.com/realDonaldTrump/status/921716470140325~ 10/21/17 12:~
    ## 4 https://twitter.com/realDonaldTrump/status/921709468055896~ 10/21/17 12:~
    ## 5 https://twitter.com/realDonaldTrump/status/921705862992887~ 10/21/17 11:~

### left\_join

``` r
# if you want to list all the data from Table1 i.e. Left table from below parameter and also wants to list all the matching data from right table i.e. table2, we can use left join
table_Left <- dplyr::left_join(table1,table2, by =c("TweetURL" = "TweetURL"))

table_Left
```

    ## # A tibble: 16 x 3
    ##    TweetURL                      TweetDate  Tweets                         
    ##    <chr>                         <chr>      <chr>                          
    ##  1 https://twitter.com/realDona~ 10/22/17 ~ Wacky Congresswoman Wilson is ~
    ##  2 https://twitter.com/realDona~ 10/22/17 ~ Doing interview today with Mar~
    ##  3 https://twitter.com/realDona~ 10/22/17 ~ ...2nd Amendment, Strong Milit~
    ##  4 https://twitter.com/realDona~ 10/22/17 ~ ...9 months than this Administ~
    ##  5 https://twitter.com/realDona~ 10/21/17 ~ I agree getting Tax Cuts appro~
    ##  6 https://twitter.com/realDona~ 10/21/17 ~ "Just out, but lightly reporte~
    ##  7 https://twitter.com/realDona~ 10/21/17 ~ Crooked Hillary Clinton spent ~
    ##  8 https://twitter.com/realDona~ 10/21/17 ~ "Keep hearing about \"tiny\" a~
    ##  9 https://twitter.com/realDona~ 10/21/17 ~ "Officials behind the now disc~
    ## 10 https://twitter.com/realDona~ 10/21/17 ~ "\x89\xdb\xcfTrump hails liber~
    ## 11 https://twitter.com/realDona~ 10/21/17 ~ Stock Market hits another all ~
    ## 12 https://twitter.com/realDona~ 10/21/17 ~ <NA>                           
    ## 13 https://twitter.com/realDona~ 10/21/17 ~ <NA>                           
    ## 14 https://twitter.com/realDona~ 10/21/17 ~ <NA>                           
    ## 15 https://twitter.com/realDona~ 10/21/17 ~ <NA>                           
    ## 16 https://twitter.com/realDona~ 10/21/17 ~ <NA>

``` r
table1
```

    ## # A tibble: 16 x 2
    ##    TweetURL                                                   TweetDate    
    ##    <chr>                                                      <chr>        
    ##  1 https://twitter.com/realDonaldTrump/status/92207065909367~ 10/22/17 12:~
    ##  2 https://twitter.com/realDonaldTrump/status/92206767670863~ 10/22/17 11:~
    ##  3 https://twitter.com/realDonaldTrump/status/92189118635228~ 10/22/17 0:09
    ##  4 https://twitter.com/realDonaldTrump/status/92188952588181~ 10/22/17 0:02
    ##  5 https://twitter.com/realDonaldTrump/status/92188824870784~ 10/21/17 23:~
    ##  6 https://twitter.com/realDonaldTrump/status/92187170756410~ 10/21/17 22:~
    ##  7 https://twitter.com/realDonaldTrump/status/92184885309098~ 10/21/17 21:~
    ##  8 https://twitter.com/realDonaldTrump/status/92182994709373~ 10/21/17 20:~
    ##  9 https://twitter.com/realDonaldTrump/status/92182828099874~ 10/21/17 19:~
    ## 10 https://twitter.com/realDonaldTrump/status/92178075837264~ 10/21/17 16:~
    ## 11 https://twitter.com/realDonaldTrump/status/92172640092261~ 10/21/17 13:~
    ## 12 https://twitter.com/realDonaldTrump/status/92172482193913~ 10/21/17 13:~
    ## 13 https://twitter.com/realDonaldTrump/status/92172330248114~ 10/21/17 13:~
    ## 14 https://twitter.com/realDonaldTrump/status/92171647014032~ 10/21/17 12:~
    ## 15 https://twitter.com/realDonaldTrump/status/92170946805589~ 10/21/17 12:~
    ## 16 https://twitter.com/realDonaldTrump/status/92170586299288~ 10/21/17 11:~

### right\_join

``` r
# if you want to list all the data from Table2 i.e. RIGHT table from below parameter and also wants to list all the matching data from left table i.e. table1, we can use right_join
table_Right <- dplyr::right_join(table1,table2, by =c("TweetURL" = "TweetURL"))

table_Right
```

    ## # A tibble: 15 x 3
    ##    TweetURL                      TweetDate  Tweets                         
    ##    <chr>                         <chr>      <chr>                          
    ##  1 https://twitter.com/realDona~ <NA>       I had a very respectful conver~
    ##  2 https://twitter.com/realDona~ <NA>       Two dozen NFL players continue~
    ##  3 https://twitter.com/realDona~ <NA>       There will be NO change to you~
    ##  4 https://twitter.com/realDona~ <NA>       It is finally sinking through.~
    ##  5 https://twitter.com/realDona~ 10/22/17 ~ Wacky Congresswoman Wilson is ~
    ##  6 https://twitter.com/realDona~ 10/22/17 ~ Doing interview today with Mar~
    ##  7 https://twitter.com/realDona~ 10/22/17 ~ ...2nd Amendment, Strong Milit~
    ##  8 https://twitter.com/realDona~ 10/22/17 ~ ...9 months than this Administ~
    ##  9 https://twitter.com/realDona~ 10/21/17 ~ I agree getting Tax Cuts appro~
    ## 10 https://twitter.com/realDona~ 10/21/17 ~ "Just out, but lightly reporte~
    ## 11 https://twitter.com/realDona~ 10/21/17 ~ Crooked Hillary Clinton spent ~
    ## 12 https://twitter.com/realDona~ 10/21/17 ~ "Keep hearing about \"tiny\" a~
    ## 13 https://twitter.com/realDona~ 10/21/17 ~ "Officials behind the now disc~
    ## 14 https://twitter.com/realDona~ 10/21/17 ~ "\x89\xdb\xcfTrump hails liber~
    ## 15 https://twitter.com/realDona~ 10/21/17 ~ Stock Market hits another all ~

``` r
table2
```

    ## # A tibble: 15 x 2
    ##    TweetURL                           Tweets                               
    ##    <chr>                              <chr>                                
    ##  1 https://twitter.com/realDonaldTru~ I had a very respectful conversation~
    ##  2 https://twitter.com/realDonaldTru~ Two dozen NFL players continue to kn~
    ##  3 https://twitter.com/realDonaldTru~ There will be NO change to your 401(~
    ##  4 https://twitter.com/realDonaldTru~ It is finally sinking through. 46% O~
    ##  5 https://twitter.com/realDonaldTru~ Wacky Congresswoman Wilson is the gi~
    ##  6 https://twitter.com/realDonaldTru~ Doing interview today with Maria Bar~
    ##  7 https://twitter.com/realDonaldTru~ ...2nd Amendment, Strong Military, I~
    ##  8 https://twitter.com/realDonaldTru~ ...9 months than this Administration~
    ##  9 https://twitter.com/realDonaldTru~ I agree getting Tax Cuts approved  i~
    ## 10 https://twitter.com/realDonaldTru~ "Just out, but lightly reported: \"F~
    ## 11 https://twitter.com/realDonaldTru~ Crooked Hillary Clinton spent hundre~
    ## 12 https://twitter.com/realDonaldTru~ "Keep hearing about \"tiny\" amount ~
    ## 13 https://twitter.com/realDonaldTru~ "Officials behind the now discredite~
    ## 14 https://twitter.com/realDonaldTru~ "\x89\xdb\xcfTrump hails liberation ~
    ## 15 https://twitter.com/realDonaldTru~ Stock Market hits another all time h~

### nest\_join

``` r
# Want to join table as nested tible use next_join 
table_Next <- dplyr::nest_join(table1,table2, by =c("TweetURL" = "TweetURL"))
table_Next
```

    ## # A tibble: 16 x 3
    ##    TweetURL                                      TweetDate     table2      
    ##  * <chr>                                         <chr>         <list>      
    ##  1 https://twitter.com/realDonaldTrump/status/9~ 10/22/17 12:~ <tibble [1 ~
    ##  2 https://twitter.com/realDonaldTrump/status/9~ 10/22/17 11:~ <tibble [1 ~
    ##  3 https://twitter.com/realDonaldTrump/status/9~ 10/22/17 0:09 <tibble [1 ~
    ##  4 https://twitter.com/realDonaldTrump/status/9~ 10/22/17 0:02 <tibble [1 ~
    ##  5 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 23:~ <tibble [1 ~
    ##  6 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 22:~ <tibble [1 ~
    ##  7 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 21:~ <tibble [1 ~
    ##  8 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 20:~ <tibble [1 ~
    ##  9 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 19:~ <tibble [1 ~
    ## 10 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 16:~ <tibble [1 ~
    ## 11 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 13:~ <tibble [1 ~
    ## 12 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 13:~ <tibble [0 ~
    ## 13 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 13:~ <tibble [0 ~
    ## 14 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 12:~ <tibble [0 ~
    ## 15 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 12:~ <tibble [0 ~
    ## 16 https://twitter.com/realDonaldTrump/status/9~ 10/21/17 11:~ <tibble [0 ~

``` r
# Joined table2 is added a tible . 
table_Next[1,]
```

    ## # A tibble: 1 x 3
    ##   TweetURL                                       TweetDate    table2       
    ##   <chr>                                          <chr>        <list>       
    ## 1 https://twitter.com/realDonaldTrump/status/92~ 10/22/17 12~ <tibble [1 x~

``` r
table_Next$url[1]
```

    ## Warning: Unknown or uninitialised column: 'url'.

    ## NULL

``` r
table_Next$table2[[1]]
```

    ## # A tibble: 1 x 1
    ##   Tweets                                                                   
    ##   <chr>                                                                    
    ## 1 Wacky Congresswoman Wilson is the gift that keeps on giving for the Repu~

``` r
# We can use Keep to keep the column name 
table_NextKeep <- dplyr::nest_join(table1,table2, by =c("TweetURL" = "TweetURL"),keep= TRUE)
table_NextKeep[1,]
```

    ## # A tibble: 1 x 3
    ##   TweetURL                                       TweetDate    table2       
    ##   <chr>                                          <chr>        <list>       
    ## 1 https://twitter.com/realDonaldTrump/status/92~ 10/22/17 12~ <tibble [1 x~

``` r
table_NextKeep$url[1]
```

    ## Warning: Unknown or uninitialised column: 'url'.

    ## NULL

``` r
table_NextKeep$table2[[1]]
```

    ## # A tibble: 1 x 2
    ##   TweetURL                           Tweets                                
    ##   <chr>                              <chr>                                 
    ## 1 https://twitter.com/realDonaldTru~ Wacky Congresswoman Wilson is the gif~

### semi\_join

``` r
#return all rows from x (let table i.e. Table 1) where there are matching values in y (right table ie.e table 2) , keeping just columns from table1.
table_Semi <- dplyr::semi_join(table1,table2, by =c("TweetURL" = "TweetURL"))
table_Semi
```

    ## # A tibble: 11 x 2
    ##    TweetURL                                                   TweetDate    
    ##    <chr>                                                      <chr>        
    ##  1 https://twitter.com/realDonaldTrump/status/92207065909367~ 10/22/17 12:~
    ##  2 https://twitter.com/realDonaldTrump/status/92206767670863~ 10/22/17 11:~
    ##  3 https://twitter.com/realDonaldTrump/status/92189118635228~ 10/22/17 0:09
    ##  4 https://twitter.com/realDonaldTrump/status/92188952588181~ 10/22/17 0:02
    ##  5 https://twitter.com/realDonaldTrump/status/92188824870784~ 10/21/17 23:~
    ##  6 https://twitter.com/realDonaldTrump/status/92187170756410~ 10/21/17 22:~
    ##  7 https://twitter.com/realDonaldTrump/status/92184885309098~ 10/21/17 21:~
    ##  8 https://twitter.com/realDonaldTrump/status/92182994709373~ 10/21/17 20:~
    ##  9 https://twitter.com/realDonaldTrump/status/92182828099874~ 10/21/17 19:~
    ## 10 https://twitter.com/realDonaldTrump/status/92178075837264~ 10/21/17 16:~
    ## 11 https://twitter.com/realDonaldTrump/status/92172640092261~ 10/21/17 13:~

forcats package
---------------

``` r
#---------------------------------

# The forcats package
# forcats is a core package in the tidyverse. It is installed via install.packages("tidyverse") and attached via  library(tidyverse). You can always load it individually via library(forcats). Main functions start with  fct_. There really is no coherent family of base functions that forcats replaces - that's why it's such a welcome addition.


data("diamonds")

str(diamonds$cut)
```

    ##  Ord.factor w/ 5 levels "Fair"<"Good"<..: 5 4 2 4 2 3 3 3 1 3 ...

``` r
# Same output with dplyr packge 

diamonds %>% 
  count(cut)
```

    ## # A tibble: 5 x 2
    ##   cut           n
    ##   <ord>     <int>
    ## 1 Fair       1610
    ## 2 Good       4906
    ## 3 Very Good 12082
    ## 4 Premium   13791
    ## 5 Ideal     21551

``` r
# Same output with forcats packge 

fct_count(diamonds$cut)
```

    ## # A tibble: 5 x 2
    ##   f             n
    ##   <ord>     <int>
    ## 1 Fair       1610
    ## 2 Good       4906
    ## 3 Very Good 12082
    ## 4 Premium   13791
    ## 5 Ideal     21551

CLI package :
-------------

\[31m——–\[39m \* CLI Package \* \[31m——–\[39m

``` r
rule(center = " * CLI Package * ", line_col = "red")
```

    ## --------  * CLI Package *  --------

``` r
rule(line = "bar2")
```

    ## ___________________________________

``` r
rule(line = "dots2")
```

    ## dots2dots2dots2dots2dots2dots2dots2

``` r
rule(center = " * RESULTS * ", col = "red")
```

    ## ----------  * RESULTS *  ----------

``` r
list_spinners()
```

    ##  [1] "dots"                "dots2"               "dots3"              
    ##  [4] "dots4"               "dots5"               "dots6"              
    ##  [7] "dots7"               "dots8"               "dots9"              
    ## [10] "dots10"              "dots11"              "dots12"             
    ## [13] "line"                "line2"               "pipe"               
    ## [16] "simpleDots"          "simpleDotsScrolling" "star"               
    ## [19] "star2"               "flip"                "hamburger"          
    ## [22] "growVertical"        "growHorizontal"      "balloon"            
    ## [25] "balloon2"            "noise"               "bounce"             
    ## [28] "boxBounce"           "boxBounce2"          "triangle"           
    ## [31] "arc"                 "circle"              "squareCorners"      
    ## [34] "circleQuarters"      "circleHalves"        "squish"             
    ## [37] "toggle"              "toggle2"             "toggle3"            
    ## [40] "toggle4"             "toggle5"             "toggle6"            
    ## [43] "toggle7"             "toggle8"             "toggle9"            
    ## [46] "toggle10"            "toggle11"            "toggle12"           
    ## [49] "toggle13"            "arrow"               "arrow2"             
    ## [52] "arrow3"              "bouncingBar"         "bouncingBall"       
    ## [55] "smiley"              "monkey"              "hearts"             
    ## [58] "clock"               "earth"               "moon"               
    ## [61] "runner"              "pong"                "shark"              
    ## [64] "dqpb"

``` r
cli::boxx("Hello there!", padding = 1, float = "center")
```

    ##         +------------------+
    ##         |                  |
    ##         |   Hello there!   |
    ##         |                  |
    ##         +------------------+
