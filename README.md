
<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->

# Lab report \#3 - instructions

Follow the instructions posted at
<https://ds202-at-isu.github.io/labs.html> for the lab assignment. The
work is meant to be finished during the lab time, but you have time
until Monday evening to polish things.

Include your answers in this document (Rmd file). Make sure that it
knits properly (into the md file). Upload both the Rmd and the md file
to your repository.

All submissions to the github repo will be automatically uploaded for
grading once the due date is passed. Submit a link to your repository on
Canvas (only one submission per team) to signal to the instructors that
you are done with your submission.

# Lab 3: Avenger’s Peril

## As a team

Extract from the data below two data sets in long form `deaths` and
`returns`

``` r
av <- read.csv("https://raw.githubusercontent.com/fivethirtyeight/data/master/avengers/avengers.csv", stringsAsFactors = FALSE)
head(av)
```

    ##                                                       URL
    ## 1           http://marvel.wikia.com/Henry_Pym_(Earth-616)
    ## 2      http://marvel.wikia.com/Janet_van_Dyne_(Earth-616)
    ## 3       http://marvel.wikia.com/Anthony_Stark_(Earth-616)
    ## 4 http://marvel.wikia.com/Robert_Bruce_Banner_(Earth-616)
    ## 5        http://marvel.wikia.com/Thor_Odinson_(Earth-616)
    ## 6       http://marvel.wikia.com/Richard_Jones_(Earth-616)
    ##                    Name.Alias Appearances Current. Gender Probationary.Introl
    ## 1   Henry Jonathan "Hank" Pym        1269      YES   MALE                    
    ## 2              Janet van Dyne        1165      YES FEMALE                    
    ## 3 Anthony Edward "Tony" Stark        3068      YES   MALE                    
    ## 4         Robert Bruce Banner        2089      YES   MALE                    
    ## 5                Thor Odinson        2402      YES   MALE                    
    ## 6      Richard Milhouse Jones         612      YES   MALE                    
    ##   Full.Reserve.Avengers.Intro Year Years.since.joining Honorary Death1 Return1
    ## 1                      Sep-63 1963                  52     Full    YES      NO
    ## 2                      Sep-63 1963                  52     Full    YES     YES
    ## 3                      Sep-63 1963                  52     Full    YES     YES
    ## 4                      Sep-63 1963                  52     Full    YES     YES
    ## 5                      Sep-63 1963                  52     Full    YES     YES
    ## 6                      Sep-63 1963                  52 Honorary     NO        
    ##   Death2 Return2 Death3 Return3 Death4 Return4 Death5 Return5
    ## 1                                                            
    ## 2                                                            
    ## 3                                                            
    ## 4                                                            
    ## 5    YES      NO                                             
    ## 6                                                            
    ##                                                                                                                                                                              Notes
    ## 1                                                                                                                Merged with Ultron in Rage of Ultron Vol. 1. A funeral was held. 
    ## 2                                                                                                  Dies in Secret Invasion V1:I8. Actually was sent tto Microverse later recovered
    ## 3 Death: "Later while under the influence of Immortus Stark committed a number of horrible acts and was killed.'  This set up young Tony. Franklin Richards later brought him back
    ## 4                                                                               Dies in Ghosts of the Future arc. However "he had actually used a hidden Pantheon base to survive"
    ## 5                                                      Dies in Fear Itself brought back because that's kind of the whole point. Second death in Time Runs Out has not yet returned
    ## 6                                                                                                                                                                             <NA>

Get the data into a format where the five columns for Death\[1-5\] are
replaced by two columns: Time, and Death. Time should be a number
between 1 and 5 (look into the function `parse_number`); Death is a
categorical variables with values “yes”, “no” and ““. Call the resulting
data set `deaths`.

Similarly, deal with the returns of characters.

Based on these datasets calculate the average number of deaths an
Avenger suffers.

``` r
library(tidyverse)
```

<<<<<<< HEAD
    ## Warning: package 'tidyverse' was built under R version 4.5.3

    ## Warning: package 'tidyr' was built under R version 4.5.3

    ## Warning: package 'readr' was built under R version 4.5.3

    ## Warning: package 'forcats' was built under R version 4.5.3

    ## Warning: package 'lubridate' was built under R version 4.5.3

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.2.0     ✔ readr     2.2.0
=======
    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.2.0     ✔ readr     2.1.6
>>>>>>> 0de536464b7d556fdb1fe6bdcd6019f453e96fb0
    ## ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ## ✔ ggplot2   4.0.2     ✔ tibble    3.3.1
    ## ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ## ✔ purrr     1.2.1     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(readr)

<<<<<<< HEAD
death <- av %>%
  pivot_longer(
    cols = starts_with("Death"),
    names_to = "Time",
    values_to = "Death") %>%
  mutate(
    Time = parse_number(Time)) %>%
  filter(Death != "") %>%
  select(-starts_with("Return"))

return <- av %>%
=======
deaths <- av %>%
  pivot_longer(
    cols = starts_with("Death"),
    names_to = "Time",
    values_to = "Death"
  ) %>%
  mutate(Time = parse_number(Time)) %>%
  filter(Death != "") %>%
  select(-starts_with("Return"))

returns <- av %>%
>>>>>>> 0de536464b7d556fdb1fe6bdcd6019f453e96fb0
  select(Name.Alias, starts_with("Return")) %>%
  pivot_longer(
    cols = starts_with("Return"),
    names_to = "Time",
<<<<<<< HEAD
    values_to = "Return") %>%
  mutate(
    Time = parse_number(Time)) %>%
  filter(Return != "")

av2 <- death %>%
  left_join(
    return,
    by = c("Name.Alias", "Time"))
```

    ## Warning in left_join(., return, by = c("Name.Alias", "Time")): Detected an unexpected many-to-many relationship between `x` and `y`.
    ## ℹ Row 71 of `x` matches multiple rows in `y`.
    ## ℹ Row 48 of `y` matches multiple rows in `x`.
    ## ℹ If a many-to-many relationship is expected, set `relationship =
    ##   "many-to-many"` to silence this warning.

``` r
head(av2)
```

    ## # A tibble: 6 × 14
    ##   URL                 Name.Alias Appearances Current. Gender Probationary.Introl
    ##   <chr>               <chr>            <int> <chr>    <chr>  <chr>              
    ## 1 http://marvel.wiki… "Henry Jo…        1269 YES      MALE   ""                 
    ## 2 http://marvel.wiki… "Janet va…        1165 YES      FEMALE ""                 
    ## 3 http://marvel.wiki… "Anthony …        3068 YES      MALE   ""                 
    ## 4 http://marvel.wiki… "Robert B…        2089 YES      MALE   ""                 
    ## 5 http://marvel.wiki… "Thor Odi…        2402 YES      MALE   ""                 
    ## 6 http://marvel.wiki… "Thor Odi…        2402 YES      MALE   ""                 
    ## # ℹ 8 more variables: Full.Reserve.Avengers.Intro <chr>, Year <int>,
    ## #   Years.since.joining <int>, Honorary <chr>, Notes <chr>, Time <dbl>,
    ## #   Death <chr>, Return <chr>

``` r
avg_deaths <- av2 %>%
  group_by(Name.Alias) %>%
  summarise(num_deaths = sum(Death == "YES")) %>%
  summarise(avg_deaths = mean(num_deaths))

avg_deaths
```

    ## # A tibble: 1 × 1
    ##   avg_deaths
    ##        <dbl>
    ## 1      0.730

=======
    values_to = "Return"
  ) %>%
  mutate(Time = parse_number(Time)) %>%
  filter(Return != "")

av2 <- deaths %>%
  left_join(
    returns,
    by = c("Name.Alias", "Time"),
    relationship = "many-to-many"
  )
```

``` r
av2 <- deaths %>%
  left_join(
    returns,
    by = c("Name.Alias", "Time"),
    relationship = "many-to-many"
  )
```

>>>>>>> 0de536464b7d556fdb1fe6bdcd6019f453e96fb0
On average, an Avenger suffers 0.73 deaths.

## Individually

For each team member, copy this part of the report.

Each team member picks one of the statements in the FiveThirtyEight
[analysis](https://fivethirtyeight.com/features/avengers-death-comics-age-of-ultron/)
and fact checks it based on the data. Use dplyr functionality whenever
possible.

### FiveThirtyEight Statement

> Quote the statement you are planning to fact-check.

## Chai’s work: The MVP of the Earth-616 Marvel Universe Avengers has to be Jocasta — an android based on Janet van Dyne and built by Ultron — who has been destroyed five times and then recovered five times.

### Include the code

Make sure to include the code to derive the (numeric) fact for the
statement

## Chai’s Work

### FiveThirtyEight Statement

> The MVP of the Earth-616 Marvel Universe Avengers has to be Jocasta —
> who has been destroyed five times and then recovered five times.

### Include the code

``` r
jocasta_deaths <- deaths %>%
  filter(str_detect(Name.Alias, "Jocasta"), toupper(Death) == "YES") %>%
  nrow()

jocasta_returns <- returns %>%
  filter(str_detect(Name.Alias, "Jocasta"), toupper(Return) == "YES") %>%
  nrow()

jocasta_deaths
```

    ## [1] 5

``` r
jocasta_returns
```

    ## [1] 5

### Include your answer

Include at least one sentence discussing the result of your
fact-checking endeavor.

Upload your changes to the repository. Discuss and refine answers as a
team.

## Nicole’s Work:

## Scott’s Work:

## Chai’s work:

<<<<<<< HEAD
\##Logan’s work: “Out of 173 listed Avengers, my analysis found that 69
had died at least one time after they joined the team.”

``` r
length(unique(av2$URL))
```

    ## [1] 173

There is 173 unique values for avengers so the number is right

``` r
deathCounts <- av2 |> group_by(URL, Name.Alias) |> summarise(numDeaths = sum(Death == "YES"))
```

    ## `summarise()` has regrouped the output.
    ## ℹ Summaries were computed grouped by URL and Name.Alias.
    ## ℹ Output is grouped by URL.
    ## ℹ Use `summarise(.groups = "drop_last")` to silence this message.
    ## ℹ Use `summarise(.by = c(URL, Name.Alias))` for per-operation grouping
    ##   (`?dplyr::dplyr_by`) instead.

``` r
deathCounts
```

    ## # A tibble: 173 × 3
    ## # Groups:   URL [173]
    ##    URL                                                      Name.Alias numDeaths
    ##    <chr>                                                    <chr>          <int>
    ##  1 http://marvel.wikia.com/2ZP45-9-X-51_(Earth-616)#        "X-51"             1
    ##  2 http://marvel.wikia.com/Abyss_(Ex_Nihilo%27s)_(Earth-61… ""                 6
    ##  3 http://marvel.wikia.com/Adam_Brashear_(Earth-616)#       "Adam Bra…         0
    ##  4 http://marvel.wikia.com/Alani_Ryan_(Earth-616)#          "Alani Ry…         0
    ##  5 http://marvel.wikia.com/Alexander_Summers_(Earth-616)#   "Alex Sum…         0
    ##  6 http://marvel.wikia.com/Alexis_(Earth-616)#              "Alexis"           0
    ##  7 http://marvel.wikia.com/Amadeus_Cho_(Earth-616)#         "Amadeus …         0
    ##  8 http://marvel.wikia.com/America_Chavez_(Earth-616)#      "America …         0
    ##  9 http://marvel.wikia.com/Angelica_Jones_(Earth-616)#      "Angelica…         0
    ## 10 http://marvel.wikia.com/Anthony_Druid_(Earth-616)#       "Anthony …         2
    ## # ℹ 163 more rows

This is the number of deaths each avenger has

``` r
atLeastOnce <- deathCounts |> filter(numDeaths > 0)
atLeastOnce
```

    ## # A tibble: 69 × 3
    ## # Groups:   URL [69]
    ##    URL                                                      Name.Alias numDeaths
    ##    <chr>                                                    <chr>          <int>
    ##  1 http://marvel.wikia.com/2ZP45-9-X-51_(Earth-616)#        "X-51"             1
    ##  2 http://marvel.wikia.com/Abyss_(Ex_Nihilo%27s)_(Earth-61… ""                 6
    ##  3 http://marvel.wikia.com/Anthony_Druid_(Earth-616)#       "Anthony …         2
    ##  4 http://marvel.wikia.com/Anthony_Stark_(Earth-616)        "Anthony …         1
    ##  5 http://marvel.wikia.com/Anthony_Stark_(Earth-96020)#     "Anthony …         1
    ##  6 http://marvel.wikia.com/Ares_(Earth-616)#                "Ares"             2
    ##  7 http://marvel.wikia.com/Barbara_Morse_(Earth-616)#       "Barbara …         1
    ##  8 http://marvel.wikia.com/Benjamin_Grimm_(Earth-616)#      "Benjamin…         1
    ##  9 http://marvel.wikia.com/Cassandra_Lang_(Earth-616)#      "Cassie L…         1
    ## 10 http://marvel.wikia.com/Clint_Barton_(Earth-616)         "Clinton …         2
    ## # ℹ 59 more rows

This gets all of the avengers that have died at least once (numDeaths !=
0)

``` r
dim(atLeastOnce)
```

    ## [1] 69  3

This has 69 rows meaning that 69 people have died at least once since
joining the Avengers. This means that the fact is correct.
=======
\##Logan’s work:
>>>>>>> 0de536464b7d556fdb1fe6bdcd6019f453e96fb0
