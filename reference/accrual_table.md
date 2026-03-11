# accrual_table

Table of recruitment overview by site, rate of recruitment

## Usage

``` r
accrual_table(
  accrual_df,
  overall = TRUE,
  name_overall = "Overall",
  pos_overall = c("last", "first"),
  unit = c("month", "year", "week", "day"),
  format_table_date = "%d%b%Y",
  format_time = "%1.0f",
  format_rrate = "%1.2f",
  header = TRUE
)
```

## Arguments

- accrual_df:

  object of class 'accrual_df' or 'accrual_list' produced by
  `accrual_create_df`.

- overall:

  logical, indicates that accrual_df contains a summary with all sites
  (only if by is not NA).

- name_overall:

  name of the summary with all sites (if by is not NA and
  overall==TRUE).

- pos_overall:

  overall in last or first row (if by is not NA and overall==TRUE).

- unit:

  time unit for time recruiting and the rate, one of `"month"`,
  `"year"`, `"week"` or `"day"`.

- format_table_date:

  format of start date in table.

- format_time:

  format of time recruiting in table.

- format_rrate:

  format of recruitment rate in table.

- header:

  include header, logical or character vector of length 4 or 5 (if
  accrual_df is a list).

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
accrual_df<-accrual_create_df(accrualdemo$date,by=accrualdemo$site)
accrual_table(accrual_df)
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

#format
accrual_table(accrual_df,format_time="%1.1f",format_rrate="%1.1f")
#>      name           start_date            time                    n
#> 1  Center First participant in Months accruing Participants accrued
#> 2  Site 1            09Jul2020             3.1                  141
#> 3  Site 2            20Jul2020             2.7                   88
#> 4  Site 3            04Sep2020             1.2                   21
#> 5 Overall            09Jul2020             3.1                  250
#>                       rate
#> 1 Accrual rate (per month)
#> 2                     46.0
#> 3                     32.6
#> 4                     18.0
#> 5                     81.5

#unit
accrual_table(accrual_df,unit="day")
#>      name           start_date          time                    n
#> 1  Center First participant in Days accruing Participants accrued
#> 2  Site 1            09Jul2020            92                  141
#> 3  Site 2            20Jul2020            81                   88
#> 4  Site 3            04Sep2020            35                   21
#> 5 Overall            09Jul2020            92                  250
#>                     rate
#> 1 Accrual rate (per day)
#> 2                   1.53
#> 3                   1.09
#> 4                   0.60
#> 5                   2.72

#common start and current dates
accrual_df<-accrual_create_df(accrualdemo$date,by=accrualdemo$site,start_date="common",
current_date="common")
accrual_table(accrual_df)
#>      name           start_date            time                    n
#> 1  Center First participant in Months accruing Participants accrued
#> 2  Site 1            09Jul2020               3                  141
#> 3  Site 2            09Jul2020               3                   88
#> 4  Site 3            09Jul2020               3                   21
#> 5 Overall            09Jul2020               3                  250
#>                       rate
#> 1 Accrual rate (per month)
#> 2                    45.98
#> 3                    28.70
#> 4                     6.85
#> 5                    81.52
accrual_df<-accrual_create_df(accrualdemo$date,by=accrualdemo$site,start_date=as.Date("2020-07-09"),
    current_date=as.Date("2020-10-15"))
accrual_table(accrual_df)
#>      name           start_date            time                    n
#> 1  Center First participant in Months accruing Participants accrued
#> 2  Site 1            09Jul2020               3                  141
#> 3  Site 2            09Jul2020               3                   88
#> 4  Site 3            09Jul2020               3                   21
#> 5 Overall            09Jul2020               3                  250
#>                       rate
#> 1 Accrual rate (per month)
#> 2                    43.16
#> 3                    26.94
#> 4                     6.43
#> 5                    76.53

```
