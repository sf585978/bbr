
bbr: basketball-reference data in R
===================================

[![Travis-CI Build Status](https://travis-ci.org/mbjoseph/bbr.svg?branch=master)](https://travis-ci.org/mbjoseph/bbr) [![Coverage Status](https://img.shields.io/codecov/c/github/mbjoseph/bbr/master.svg)](https://codecov.io/github/mbjoseph/bbr?branch=master) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/bbr)](https://cran.r-project.org/package=bbr) [![Licence](https://img.shields.io/badge/licence-GPL--3-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-3.0.html) [![Last-changedate](https://img.shields.io/badge/last%20change-2018--01--27-brightgreen.svg)](/commits/master)

<!-- README.md is generated from README.Rmd. Please edit that file -->
The bbr package is designed to quickly fetch tidy data from www.basketball-reference.com. This package is actively under development and the interface will change as new features are added.

Installation
------------

``` r
devtools::install_github("mbjoseph/bbr")
```

Example usage
-------------

The `get_season` function retrieves season summary data for one season.

``` r
library(bbr)

ninetyone <- get_season(1991)
str(ninetyone)
```

    ## 'data.frame':    441 obs. of  31 variables:
    ##  $ player     : chr  "Alaa Abdelnaby" "Mahmoud Abdul-Rauf" "Mark Acres" "Michael Adams" ...
    ##  $ pos        : chr  "PF" "PG" "C" "PG" ...
    ##  $ age        : num  22 21 28 28 31 31 27 26 26 26 ...
    ##  $ tm         : chr  "POR" "DEN" "ORL" "DEN" ...
    ##  $ g          : num  43 67 68 66 78 80 42 34 68 26 ...
    ##  $ gs         : num  0 19 0 66 13 0 1 0 2 0 ...
    ##  $ mp         : num  290 1505 1313 2346 2006 ...
    ##  $ fg         : num  55 417 109 560 420 337 99 59 116 27 ...
    ##  $ fga        : num  116 1009 214 1421 909 ...
    ##  $ fg_pct     : num  0.474 0.413 0.509 0.394 0.462 0.472 0.44 0.504 0.43 0.37 ...
    ##  $ three_p    : num  0 24 1 167 24 102 5 7 0 0 ...
    ##  $ three_pa   : num  0 100 3 564 78 251 21 23 1 1 ...
    ##  $ three_p_pct: num  NA 0.24 0.333 0.296 0.308 0.406 0.238 0.304 0 0 ...
    ##  $ two_p      : num  55 393 108 393 396 235 94 52 116 27 ...
    ##  $ two_pa     : num  116 909 211 857 831 463 204 94 269 72 ...
    ##  $ two_p_pct  : num  0.474 0.432 0.512 0.459 0.477 0.508 0.461 0.553 0.431 0.375 ...
    ##  $ efg_pct    : num  0.474 0.425 0.512 0.453 0.475 0.543 0.451 0.534 0.43 0.37 ...
    ##  $ ft         : num  25 84 66 465 240 114 41 26 60 16 ...
    ##  $ fta        : num  44 98 101 529 317 138 48 31 115 28 ...
    ##  $ ft_pct     : num  0.568 0.857 0.653 0.879 0.757 0.826 0.854 0.839 0.522 0.571 ...
    ##  $ orb        : num  27 34 140 58 134 45 41 10 97 26 ...
    ##  $ drb        : num  62 87 219 198 240 160 76 14 221 49 ...
    ##  $ trb        : num  89 121 359 256 374 205 117 24 318 75 ...
    ##  $ ast        : num  12 206 25 693 139 285 45 22 16 3 ...
    ##  $ stl        : num  4 55 25 147 47 63 15 8 35 8 ...
    ##  $ blk        : num  12 4 25 6 20 13 8 1 45 9 ...
    ##  $ tov        : num  22 110 42 240 128 100 40 16 84 22 ...
    ##  $ pf         : num  39 149 218 162 209 195 88 11 140 29 ...
    ##  $ pts        : num  135 942 285 1752 1104 ...
    ##  $ start_year : num  1990 1990 1990 1990 1990 1990 1990 1990 1990 1990 ...
    ##  $ end_year   : num  1991 1991 1991 1991 1991 ...

The `get_players` function gets player data for individuals by last initial.

``` r
a_data <- get_players("A")
str(a_data)
```

    ## 'data.frame':    158 obs. of  9 variables:
    ##  $ player    : chr  "Alaa Abdelnaby" "Zaid Abdul-Aziz" "Kareem Abdul-Jabbar" "Mahmoud Abdul-Rauf" ...
    ##  $ from      : int  1991 1969 1970 1991 1998 1997 1977 1957 1947 2017 ...
    ##  $ to        : int  1995 1978 1989 2001 2003 2008 1981 1957 1948 2018 ...
    ##  $ pos       : chr  "F-C" "C-F" "C" "G" ...
    ##  $ ht        : chr  "6-10" "6-9" "7-2" "6-1" ...
    ##  $ wt        : int  240 235 225 162 223 225 220 180 195 190 ...
    ##  $ birth_date: chr  "June 24, 1968" "April 7, 1946" "April 16, 1947" "March 9, 1969" ...
    ##  $ college   : chr  "Duke University" "Iowa State University" "University of California, Los Angeles" "Louisiana State University" ...
    ##  $ slug      : chr  "abdelal01" "abdulza01" "abdulka01" "abdulma02" ...

The `get_player_data` function returns data for each season that a player played. As an argument, this function takes a slug for the player you're interested in. This can be found using the `get_players()` function, and is part of the URL to the data of a player, e.g., if the URL is <https://www.basketball-reference.com/players/a/abdelal01.html> then the slug is abdelal01.

``` r
abdelnaby_d <- get_player_data('abdelal01')
str(abdelnaby_d)
```

    ## 'data.frame':    9 obs. of  32 variables:
    ##  $ player     : chr  "Alaa Abdelnaby" "Alaa Abdelnaby" "Alaa Abdelnaby" "Alaa Abdelnaby" ...
    ##  $ season     : chr  "1990-91" "1991-92" "1992-93" "1992-93" ...
    ##  $ age        : int  22 23 24 24 24 25 26 26 26
    ##  $ tm         : chr  "POR" "POR" "TOT" "MIL" ...
    ##  $ lg         : chr  "NBA" "NBA" "NBA" "NBA" ...
    ##  $ pos        : chr  "PF" "PF" "PF" "PF" ...
    ##  $ g          : int  43 71 75 12 63 13 54 51 3
    ##  $ gs         : int  0 1 52 0 52 0 0 0 0
    ##  $ mp         : num  6.7 13.2 17.5 13.3 18.3 12.2 9.4 9.3 10
    ##  $ fg         : num  1.3 2.5 3.3 2.2 3.5 1.8 2.2 2.3 0.3
    ##  $ fga        : num  2.7 5.1 6.3 4.7 6.6 4.2 4.3 4.3 3.7
    ##  $ fg_pct     : num  0.474 0.493 0.518 0.464 0.525 0.436 0.511 0.532 0.091
    ##  $ three_p    : num  0 0 0 0 0 0 0 0 0
    ##  $ three_pa   : num  0 0 0 0.1 0 0 0 0 0
    ##  $ three_p_pct: num  NA NA 0 0 NA NA 0 0 NA
    ##  $ two_p      : num  1.3 2.5 3.3 2.2 3.5 1.8 2.2 2.3 0.3
    ##  $ two_pa     : num  2.7 5.1 6.3 4.6 6.6 4.2 4.2 4.3 3.7
    ##  $ two_p_pct  : num  0.474 0.493 0.519 0.473 0.525 0.436 0.515 0.537 0.091
    ##  $ efg_pct    : num  0.474 0.493 0.518 0.464 0.525 0.436 0.511 0.532 0.091
    ##  $ ft         : num  0.6 1.1 1.2 1 1.2 1.2 0.4 0.4 0
    ##  $ fta        : num  1 1.4 1.5 1.3 1.6 1.9 0.6 0.7 0
    ##  $ ft_pct     : num  0.568 0.752 0.759 0.75 0.76 0.64 0.571 0.571 NA
    ##  $ orb        : num  0.6 1.1 1.7 1 1.8 0.9 0.7 0.7 1
    ##  $ drb        : num  1.4 2.5 2.8 2.1 3 2.6 1.4 1.4 1.7
    ##  $ trb        : num  2.1 3.7 4.5 3.1 4.8 3.5 2.1 2.1 2.7
    ##  $ ast        : num  0.3 0.4 0.4 0.8 0.3 0.2 0.2 0.3 0
    ##  $ stl        : num  0.1 0.4 0.3 0.5 0.3 0.2 0.3 0.3 0
    ##  $ blk        : num  0.3 0.2 0.3 0.3 0.3 0.2 0.2 0.2 0
    ##  $ tov        : num  0.5 0.9 1.3 1.1 1.3 1.3 0.8 0.8 1.7
    ##  $ pf         : num  0.9 1.9 2.5 2 2.6 1.5 1.9 2 0.7
    ##  $ pts        : num  3.1 6.1 7.7 5.3 8.2 4.9 4.7 5 0.7
    ##  $ slug       : chr  "abdelal01" "abdelal01" "abdelal01" "abdelal01" ...
