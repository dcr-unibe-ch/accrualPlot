# Print methods for accrual objects

Print methods for accrual objects

## Usage

``` r
# S3 method for class 'accrual_df'
print(x, head = TRUE, ...)

# S3 method for class 'accrual_list'
print(x, ...)
```

## Arguments

- x:

  object of class 'accrual_df' or 'accrual_list' produced by
  accrual_create_df.

- head:

  show header of the accrual data?

- ...:

  arguments passed to head

## Value

No return value

## Examples

``` r
data(accrualdemo)
accrual_df<-accrual_create_df(accrualdemo$date)
print(accrual_df)
#> 250 participants recruited between 2020-07-09 and 2020-10-09 
#>         Date Freq Cumulative
#> 1 2020-07-09    0          0
#> 2 2020-07-09    1          1
#> 3 2020-07-14    3          4
#> 4 2020-07-16    1          5
#> 5 2020-07-19    1          6
#> 6 2020-07-20    1          7
# only show text
print(accrual_df, head = FALSE)
#> 250 participants recruited between 2020-07-09 and 2020-10-09 
# show first 15 days
print(accrual_df, n = 15)
#> 250 participants recruited between 2020-07-09 and 2020-10-09 
#>          Date Freq Cumulative
#> 1  2020-07-09    0          0
#> 2  2020-07-09    1          1
#> 3  2020-07-14    3          4
#> 4  2020-07-16    1          5
#> 5  2020-07-19    1          6
#> 6  2020-07-20    1          7
#> 7  2020-07-21    2          9
#> 8  2020-07-22    1         10
#> 9  2020-07-23    4         14
#> 10 2020-07-25    1         15
#> 11 2020-07-26    1         16
#> 12 2020-07-27    2         18
#> 13 2020-07-30    1         19
#> 14 2020-07-31    3         22
#> 15 2020-08-02    3         25
```
