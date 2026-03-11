# Summary method for accrual_dfs (as created by accrual_create_df)

Summary method for accrual_dfs (as created by accrual_create_df)

## Usage

``` r
# S3 method for class 'accrual_df'
summary(object, ...)
```

## Arguments

- object:

  object of class 'accrual_df' or 'accrual_list' produced by
  accrual_create_df.

- ...:

  options passed to other functions

## Value

Returns data frame with a header, a row per site and overall and the
following columns:

- name:

  name of the site (if accrual_df is a list)

- start_date:

  accrual start date

- time:

  time accruing

- n:

  number of patients accrued

- rate:

  accrual rate per time unit

## Examples

``` r
data(accrualdemo)
accrual_df<-accrual_create_df(accrualdemo$date, accrualdemo$site)
summary(accrual_df)
#>      name           start_date            time                    n
#> 1  Center First participant in Months accruing Participants accrued
#> 2  Site 1            09Jul2020               3                  141
#> 3  Site 2            20Jul2020               3                   88
#> 4  Site 3            04Sep2020               1                   21
#> 5 Overall            09Jul2020               3                  250
#>                       rate
#> 1 Accrual rate (per month)
#> 2                    45.98
#> 3                    32.59
#> 4                    18.00
#> 5                    81.52
```
