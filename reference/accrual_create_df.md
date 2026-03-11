# accrual_create_df

Creates a data frame or a list of data frames that contains the absolute
and cumululative number of participants recruited at each date from a
vector with enrollment dates. Used as input for accrual plot functions.

## Usage

``` r
accrual_create_df(
  enrollment_dates,
  by = NA,
  start_date = "site",
  current_date = "common",
  overall = TRUE,
  name_overall = "Overall",
  pos_overall = c("last", "first"),
  force_start0 = TRUE
)
```

## Arguments

- enrollment_dates:

  date vector with one entry per participants.

- by:

  factor or character vector with sites, has to have the same length as
  enrollment dates. If not NA, a list with an accrual data frame for
  each site is generated.

- start_date:

  date when recruitment started. Single date (used for all sites in by),
  named date vector (with length and names corresponding to the levels
  of by), "common" (first date overall) or "site" (first date for each
  site, default).

- current_date:

  date of the data export or database freeze. Single date, named date
  vector (with length and names corresponding to the levels of by),
  "common" (last date overall, default) or "site" (last date for each
  site).

- overall:

  logical indicates that accrual_df contains a summary with all sites
  (only if by is not NA).

- name_overall:

  name of the summary with all sites (if by is not NA and
  overall==TRUE).

- pos_overall:

  overall as last or first element of the list (if by is not NA and
  overall==TRUE).

- force_start0:

  logical, adds an extra 0 line to the accrual data frame in cases where
  a start date is given and corresponds to the earliest enrollment date.

## Value

Returns a data frame of class 'accrual_df' or a list of class
'accrual_list' with an 'accrual_df' for each level of by (if by is not
NA). The 'accrual_df' contains a row per accrual day and the following
three columns:

- Date:

  date of accrual

- Freq:

  absolute number accrued at Date

- Cumulative:

  cumulative number accrued up to Date

## See also

[`accrual_plot_cum()`](accrual_plot_cum.md),
[`accrual_plot_abs()`](accrual_plot_abs.md) and
[`accrual_plot_predict()`](accrual_plot_predict.md) to generate
cumulative, absolute and prediction plots, and
[`accrual_table()`](accrual_table.md) to generate an accrual table.

## Examples

``` r
# \donttest{
data(accrualdemo)
accrual_create_df(accrualdemo$date)
#> 250 participants recruited between 2020-07-09 and 2020-10-09 
#>         Date Freq Cumulative
#> 1 2020-07-09    0          0
#> 2 2020-07-09    1          1
#> 3 2020-07-14    3          4
#> 4 2020-07-16    1          5
#> 5 2020-07-19    1          6
#> 6 2020-07-20    1          7
# different start and current date
accrual_create_df(accrualdemo$date, start_date=as.Date("2020-07-08"),
current_date=as.Date("2020-10-15"))
#> 250 participants recruited between 2020-07-08 and 2020-10-15 
#>         Date Freq Cumulative
#> 1 2020-07-08    0          0
#> 2 2020-07-09    1          1
#> 3 2020-07-14    3          4
#> 4 2020-07-16    1          5
#> 5 2020-07-19    1          6
#> 6 2020-07-20    1          7

#by site
accrual_create_df(accrualdemo$date,by=accrualdemo$site)
#> Site 1:
#> 141 participants recruited between 2020-07-09 and 2020-10-09 
#>         Date Freq Cumulative
#> 1 2020-07-09    0          0
#> 2 2020-07-09    1          1
#> 3 2020-07-14    3          4
#> 4 2020-07-16    1          5
#> 5 2020-07-19    1          6
#> 6 2020-07-21    1          7
#> 
#> Site 2:
#> 88 participants recruited between 2020-07-20 and 2020-10-09 
#>         Date Freq Cumulative
#> 1 2020-07-20    0          0
#> 2 2020-07-20    1          1
#> 3 2020-07-21    1          2
#> 4 2020-07-22    1          3
#> 5 2020-07-23    1          4
#> 6 2020-07-26    1          5
#> 
#> Site 3:
#> 21 participants recruited between 2020-09-04 and 2020-10-09 
#>         Date Freq Cumulative
#> 1 2020-09-04    0          0
#> 2 2020-09-04    1          1
#> 3 2020-09-05    1          2
#> 4 2020-09-07    2          4
#> 5 2020-09-12    1          5
#> 6 2020-09-13    1          6
#> 
#> Overall:
#> 250 participants recruited between 2020-07-09 and 2020-10-09 
#>         Date Freq Cumulative
#> 1 2020-07-09    0          0
#> 2 2020-07-09    1          1
#> 3 2020-07-14    3          4
#> 4 2020-07-16    1          5
#> 5 2020-07-19    1          6
#> 6 2020-07-20    1          7
#> 
# }
```
