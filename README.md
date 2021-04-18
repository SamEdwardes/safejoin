
<!-- README.md is generated from README.Rmd. Please edit that file -->

# safejoin

The goal of safejoin is to guarantee that when performing joins that
extra rows are not added to your data. safejoin is a wrapper around the
[`dplyr::left_join`](https://dplyr.tidyverse.org/reference/join.html)
function.

-   [Docs](https://safejoin-r.netlify.app/)
-   [GitHub](https://github.com/SamEdwardes/safejoin/)
-   CRAN (not yet published)

## Installation

safejoin is currently under development.

<!--
You can install the released version of safejoin from [CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("safejoin")
```
-->

## Example

Depending on your need safejoin can raise an error, a warning, or a
message. By default safejoin will raise an error.

**Error**:

``` r
library(safejoin)
x <- data.frame(key = c("a", "b"), value_x = c(1, 2))
y <- data.frame(key = c("a", "a"), value_y = c(1, 1))
safe_left_join(x, y, by = "key")
#> Error in safe_left_join(x, y, by = "key"): Input data x had 2 rows. After performing the join the data has 3 rows.
```

**Warning**:

``` r
safe_left_join(x, y, by = "key", action="warning")
#> Warning in safe_left_join(x, y, by = "key", action = "warning"): Input data x
#> had 2 rows. After performing the join the data has 3 rows.
#>   key value_x value_y
#> 1   a       1       1
#> 2   a       1       1
#> 3   b       2      NA
```

**Message**:

``` r
safe_left_join(x, y, by = "key", action="message")
#> Input data x had 2 rows. After performing the join the data has 3 rows.
#>   key value_x value_y
#> 1   a       1       1
#> 2   a       1       1
#> 3   b       2      NA
```

When a join is “safe” `safe_left_join` will have the exact same behavior
as
[`dplyr::left_join`](https://dplyr.tidyverse.org/reference/join.html).

``` r
x <- data.frame(key = c("a", "b"), value_x = c(1, 2))
y <- data.frame(key = c("a", "b"), value_y = c(1, 1))
safe_left_join(x, y, by = "key")
#>   key value_x value_y
#> 1   a       1       1
#> 2   b       2       1
```
