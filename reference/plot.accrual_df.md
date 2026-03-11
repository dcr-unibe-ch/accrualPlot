# Plot method for accrual data frames produced by `accrual_create_df`

Plot method for accrual data frames produced by `accrual_create_df`

## Usage

``` r
# S3 method for class 'accrual_df'
plot(x, which = "cum", engine = c("base", "ggplot2"), ...)
```

## Arguments

- x:

  object of class 'accrual_df' or 'accrual_list' produced by
  accrual_create_df.

- which:

  one of `"cumulative"`, `"absolute"` or `"predict"`. Abbreviations are
  allowed.

- engine:

  string to indicate the plotting engine (base/graphics or ggplot2)

- ...:

  options passed to other functions

## Value

A plot with cumulative or absolute accrual, or accrual prediction.

## See also

[`accrual_plot_abs()`](accrual_plot_abs.md),
[`accrual_plot_cum()`](accrual_plot_cum.md) and
[`accrual_plot_predict()`](accrual_plot_predict.md)

## Examples

``` r
data(accrualdemo)
accrual_df <- accrual_create_df(accrualdemo$date)
plot(accrual_df)

plot(accrual_df, "abs", unit="week")

plot(accrual_df, "pred", target = 300)

plot(accrual_df, "pred", target = 300, engine = "ggplot")
#> Warning: All aesthetics have length 1, but the data has 79 rows.
#> ℹ Please consider using `annotate()` or provide this layer with data containing
#>   a single row.
```
