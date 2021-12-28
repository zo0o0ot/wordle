
<!-- README.md is generated from README.Rmd. Please edit that file -->

# wordle

<!-- badges: start -->

![](https://img.shields.io/badge/cool-useless-green.svg)
[![R-CMD-check](https://github.com/coolbutuseless/wordle/workflows/R-CMD-check/badge.svg)](https://github.com/coolbutuseless/wordle/actions)
<!-- badges: end -->

The `{wordle}` package contains code to assist in finding good candidate
words for Wordle.

`Wordle` itself is a guess-a-word puzzle [playable
online](https://www.powerlanguage.co.uk/wordle/).

There’s a small [article in The
Guardian](https://www.theguardian.com/games/2021/dec/23/what-is-wordle-the-new-viral-word-game-delighting-the-internet)
about it.

The game plays like the old ‘mastermind’ board game, but with letters
instead of coloured pins. The gameplay is as follows:

1.  Enter a word as a guess for the hidden target word.
2.  Any letters which are within the hidden target word are coloured in
    yellow.
3.  Any letters which match exactly the letter in the hidden target word
    are coloured green
4.  Figure out a new candidate word as a guess for the hidden target
    word, and go back to Step 1.

In the following game of Wordle, the first guess was `eaten`, the second
was `arise`, and then the third guess really only has one good option
given the constraints revealed so far: `aside` (which was the hidden
target word).

<img src="man/figures/eg.png" />

The process of finding good candidate words given what letters have been
seen so far is a good match for regular expressions. This package aims
to help you find these good candidate words.

## What’s in the box

-   `Wordle` R6 Class with methods:
    -   `$new()` to start a new object to help with a new puzzle.
    -   `$get_suggestions()` to get a list of candidate words given the
        words and responses that have been seen so far
    -   `$update()` to notify the object of what the latest `word` was,
        and the colour responses received back from the game for each
        letter.

## Installation

You can install from [GitHub](https://github.com/coolbutuseless/wordle)
with:

``` r
# install.package('remotes')
remotes::install_github('coolbutuseless/wordle')
```

# Puzzle - What’s my first guess?

<img src="man/figures/00.png" />

``` r
wordle <- Wordle$new(nchar = 5)
wordle$get_suggestions()
#>  [1] "otate" "tatta" "tenet" "eaten" "enate" "tatie" "teest" "teste" "setae"
#> [10] "tease" "teeth" "theet" "state" "taste" "testa" "arete" "atone" "eater"
#> [19] "neese" "oaten"
```

## Guess `eaten`

There’s a lot of weird words in the word list, so use a bit of common
sense to pick out a likely word - in this case: `eaten`

<img src="man/figures/01.png" />

``` r
wordle$update("eaten", c('yellow', 'grey', 'grey', 'grey', 'grey'))
wordle$get_suggestions()
#>  [1] "hoose" "hoise" "issei" "osier" "serio" "diose" "idose" "loose" "oside"
#> [10] "ohelo" "rodeo" "shies" "helio" "horse" "roleo" "shoer" "shore" "cooer"
#> [19] "diode" "hirse"
```

## Guess `rodeo`

<img src="man/figures/02.png" />

``` r
wordle$update("rodeo", c('yellow', 'grey', 'grey', 'yellow', 'grey'))
wordle$get_suggestions()
#>  [1] "hirse" "shire" "cheir" "cress" "swire" "crile" "serif" "shure" "cerci"
#> [10] "ceric" "girse" "curie" "ferri" "freir" "meril" "ureic" "crime" "fresh"
#> [19] "spire" "birse"
```

## Guess `shire`

<img src="man/figures/03.png" />

``` r
wordle$update("shire", c('grey', 'grey', 'grey', 'green', 'yellow'))
wordle$get_suggestions()
#>  [1] "merry" "ferry" "clerk" "perry" "berry" "lyery" "kerry" "querl" "becry"
#> [10] "jerry" "query" "Jerry" "Jewry" "Kerry" "Perry"
```

## Guess `merry`

<img src="man/figures/04.png" />

``` r
wordle$update("merry", c('grey', 'green', 'green', 'green', 'green'))
wordle$get_suggestions()
#> [1] "ferry" "perry" "berry" "kerry" "jerry" "Jerry" "Kerry" "Perry"
```

## Guess `ferry`

<img src="man/figures/05.png" />

**Success!**

## Acknowledgements

-   R Core for developing and maintaining the language.
-   CRAN maintainers, for patiently shepherding packages onto CRAN and
    maintaining the repository
