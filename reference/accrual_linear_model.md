# accrual_linear_model

Creates a weighted linear regression model using an accrual data frame
produced by `accrual_create_df`.

## Usage

``` r
accrual_linear_model(
  accrual_df,
  fill_up = TRUE,
  wfun = function(x) seq(1/nrow(x), 1, by = 1/nrow(x))
)
```

## Arguments

- accrual_df:

  object of class 'accrual_df' or 'accrual_list' produced by
  `accrual_create_df`.

- fill_up:

  whether to fill up days where no recruitment was observed,

- wfun:

  function to calculate the weights with accrual data frame as argument,
  default is wfun\<-function(x) seq(1 / nrow(x), 1, by = 1/nrow(x)).

## Value

Returns an object of class 'lm' with a weighted linear regression of
cumulative accrual on dates.

## Examples

``` r
# \donttest{
data(accrualdemo)
accrual_df<-accrual_create_df(accrualdemo$date)
accrual_linear_model(accrual_df)
#> 
#> Call:
#> lm(formula = Cumulative ~ Date, data = accrual_dfi, weights = weivec)
#> 
#> Coefficients:
#> (Intercept)         Date  
#>  -65341.023        3.537  
#> 

#unweighted
accrual_linear_model(accrual_df, wfun=function(x) rep(1,nrow(x)))
#> 
#> Call:
#> lm(formula = Cumulative ~ Date, data = accrual_dfi, weights = weivec)
#> 
#> Coefficients:
#> (Intercept)         Date  
#>  -54614.315        2.957  
#> 

#different start and current date
accrual_df<-accrual_create_df(accrualdemo$date,start_date=as.Date("2020-07-08"),
    current_date=as.Date("2020-07-15"))
#> Warning: Current date is before last recruitment and will not be used.
accrual_linear_model(accrual_df)
#> 
#> Call:
#> lm(formula = Cumulative ~ Date, data = accrual_dfi, weights = weivec)
#> 
#> Coefficients:
#> (Intercept)         Date  
#>  -64704.911        3.502  
#> 

#accrual_df with by option
accrual_df<-accrual_create_df(accrualdemo$date,by=accrualdemo$site)
accrual_linear_model(accrual_df)
#> $`Site 1`
#> 
#> Call:
#> lm(formula = Cumulative ~ Date, data = accrual_dfi, weights = weivec)
#> 
#> Coefficients:
#> (Intercept)         Date  
#>  -36055.515        1.952  
#> 
#> 
#> $`Site 2`
#> 
#> Call:
#> lm(formula = Cumulative ~ Date, data = accrual_dfi, weights = weivec)
#> 
#> Coefficients:
#> (Intercept)         Date  
#>  -23799.342        1.288  
#> 
#> 
#> $`Site 3`
#> 
#> Call:
#> lm(formula = Cumulative ~ Date, data = accrual_dfi, weights = weivec)
#> 
#> Coefficients:
#> (Intercept)         Date  
#>  -1.082e+04    5.845e-01  
#> 
#> 
#> $Overall
#> 
#> Call:
#> lm(formula = Cumulative ~ Date, data = accrual_dfi, weights = weivec)
#> 
#> Coefficients:
#> (Intercept)         Date  
#>  -65341.023        3.537  
#> 
#> 
# }
```
