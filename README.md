
<!-- README.md is generated from README.Rmd. Please edit that file -->

# sgplot <img src="man/figures/logo.svg" alt="sgplot logo" align="right" height="150"/>

<!-- badges: start -->

[![GitHub release (latest by
date)](https://img.shields.io/github/v/release/DataScienceScotland/sgplot)](https://github.com/DataScienceScotland/sgplot/releases/latest)
[![R build
status](https://github.com/DataScienceScotland/sgplot/workflows/R-CMD-check/badge.svg)](https://github.com/DataScienceScotland/sgplot/actions)

<!-- badges: end -->

sgplot is an R package for creating accessible plots in the Scottish
Government. Currently, functions are available for styling ggplot2
plots.

The package has been developed using the [Government Analysis
Function](https://analysisfunction.civilservice.gov.uk/) Data
Visualisation guidance for
[charts](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-charts/)
and
[colours](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-colours-in-charts/).
sgplot should be used in conjunction with these guidance documents.

More information about the package and its functions can be found on the
[sgplot website](https://DataScienceScotland.github.io/sgplot). In
particular, the
[cookbook](https://DataScienceScotland.github.io/sgplot/articles/cookbook.html)
contains lots of examples.

## Installation

If you are working within the Scottish Government network, you can
install sgplot in the same way as with other R packages. The easiest way
to do this is by using the
[pkginstaller](https://github.com/DataScienceScotland/pkginstaller/tree/main)
add-in. Further guidance is available on
[eRDM](https://erdm.scotland.gov.uk:8443/documents/A42404229/details).

Alternatively, sgplot can be installed directly from GitHub. Note that
this method requires the remotes package and may not work from within
the Scottish Government network.

``` r
remotes::install_github(
  "DataScienceScotland/sgplot",
  upgrade = "never",
  build_vignettes = TRUE
)
```

Finally, sgplot can also be installed by downloading the [zip of the
repository](https://github.com/DataScienceScotland/sgplot/archive/main.zip)
and running the following code, replacing the section marked `<>`
(including the arrows themselves) with the location of the downloaded
zip:

``` r
remotes::install_local(
  "<FILEPATH OF ZIPPED FILE>/sgplot-main.zip",
  upgrade = "never",
  build_vignettes = TRUE
)
```

## Getting Started

Once installed, sgplot can be loaded using the `library()` function:

``` r
library(sgplot)
```

Help files for each function in the package can be found on the
[References](https://datasciencescotland.github.io/sgplot/reference)
page of the package website. Alternatively, type `?function_name` into
the RStudio console. For example:

``` r
?theme_sg()
```

### Use sgplot as default

The easiest way to use sgplot is by adding `use_sgplot()` to the
beginning of your R script, Rmarkdown document or Shiny app code. This
function will set a number of defaults to ggplot2 geoms, use sgplot
colour palettes and use `theme_sg()`.

#### Example 1: Plot with one colour using ggplot2 defaults

``` r
library(ggplot2)
library(dplyr)
library(gapminder)

gapminder |> 
  filter(year == 2007 & continent == "Europe") |>
  slice_max(order_by = lifeExp, n = 5) |>
  ggplot() +
  geom_col(aes(x = reorder(country, -lifeExp), y = lifeExp)) +
  scale_y_continuous(expand = c(0, 0)) +
  labs(
    x = NULL,
    y = NULL,
    title = "Iceland has the highest life expectancy in Europe",
    subtitle = "Life expectancy in European countries, 2007",
    caption = "Source: Gapminder"
  )
```

<img src="man/figures/README-ex1-1.svg" alt="A bar chart with grey background, white grid lines and dark grey bars."  />

#### Example 2: Plot with one colour using sgplot defaults

``` r
sgplot::use_sgplot()

gapminder |> 
  filter(year == 2007 & continent == "Europe") |>
  slice_max(order_by = lifeExp, n = 5) |>
  ggplot() +
  geom_col(aes(x = reorder(country, -lifeExp), y = lifeExp)) +
  scale_y_continuous(expand = c(0, 0)) +
  labs(
    x = NULL,
    y = NULL,
    title = "Iceland has the highest life expectancy in Europe",
    subtitle = "Life expectancy in European countries, 2007",
    caption = "Source: Gapminder"
  )
```

<img src="man/figures/README-ex2-1.svg" alt="A bar chart with white background, light grey horizontal grid lines dark blue bars."  />

**Note on use of titles, subtitles and captions** <br> Titles, subtitles
and captions have been embedded in these example charts for
demonstration purposes. However, for accessibility reasons, it is
usually preferable to provide titles in the body of the page rather than
embedded within the image of the plot. More information is available in
the [accessibility
article](https://datasciencescotland.github.io/sgplot/articles/accessibility.html#other-accessibility-considerations).

## Licence

Unless stated otherwise, the codebase is released under [the MIT
License](LICENSE). This covers both the codebase and any sample code in
the documentation.

The documentation is [© Crown
copyright](http://www.nationalarchives.gov.uk/information-management/re-using-public-sector-information/uk-government-licensing-framework/crown-copyright/)
and available under the terms of the [Open Government
3.0](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)
licence.
