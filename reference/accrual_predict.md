# accrual_predict

accrual_predict

## Usage

``` r
accrual_predict(accrual_df, accrual_fit, target)
```

## Arguments

- accrual_df:

  accrual data frame produced by `accrual_create_df` (optionally with by
  option as a list)

- accrual_fit:

  linear model produced by accrual_linear_model, can be a list with the
  same length as accrual_df

- target:

  target sample size or date to predict end date or expected sample
  size, respectively. A single number or date, or a named vector with
  the same length as accrual_df (to add site-specific targets).

## Value

Returns the predicted end date(s) or the predicted sample size(s).

## Details

Prediction of end date based on an accrual data frame produced by
`accrual_create_df`, a fitted regression model produced by
accrual_linear_model and a target sample size.

## Examples

``` r
# \donttest{
data(accrualdemo)
accrual_df<-accrual_create_df(accrualdemo$date)
accrual_model<-accrual_linear_model(accrual_df)
#predict date for a specific n
accrual_predict(accrual_df,accrual_model,target=300)
#> [1] "2020-10-24"
#predict n at a specific date
accrual_predict(accrual_df,accrual_model,target=as.Date("2020-11-01"))
#> [1] 331.3405

#different start and current date
accrual_df<-accrual_create_df(accrualdemo$date,start_date=as.Date("2020-07-09"),
    current_date=as.Date("2020-10-15"))
accrual_model<-accrual_linear_model(accrual_df)
accrual_predict(accrual_df,accrual_model,target=300)
#> [1] "2020-10-30"

 #accrual_df with by option
 accrual_df<-accrual_create_df(accrualdemo$date,by=accrualdemo$site)
accrual_model<-accrual_linear_model(accrual_df)
accrual_predict(accrual_df,accrual_model,
  target=c("Site 1"=160,"Site 2"=100,"Site 3"=40,"Overall"=300))
#> $`Site 1`
#>       Site 1 
#> "2020-10-19" 
#> 
#> $`Site 2`
#>       Site 2 
#> "2020-10-19" 
#> 
#> $`Site 3`
#>       Site 3 
#> "2020-11-11" 
#> 
#> $Overall
#>      Overall 
#> "2020-10-24" 
#> 
accrual_predict(accrual_df,accrual_model,target=as.Date("2020-11-01"))
#> $`Site 1`
#> [1] 185.8957
#> 
#> $`Site 2`
#> [1] 117.6193
#> 
#> $`Site 3`
#> [1] 34.44371
#> 
#> $Overall
#> [1] 331.3405
#> 
# }
```
