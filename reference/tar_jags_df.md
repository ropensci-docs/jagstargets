# Select a strategic piece of `R2jags` output.

Not a user-side function. Do not call directly. Exported for
infrastructure reasons only.

## Usage

``` r
tar_jags_df(
  fit,
  data,
  output = c("draws", "summary", "dic"),
  variables = NULL,
  summaries = NULL,
  summary_args = NULL,
  transform = NULL
)
```

## Arguments

- fit:

  `R2jags` object.

- data:

  A list, the original JAGS dataset.

- output:

  Character of length 1 denoting the type of output `tibble` to return:
  `"draws"` for MCMC samples (which could take up a lot of space)
  `"summary"` for lightweight posterior summary statistics, and `"dic"`
  for the overall deviance information criterion and effective number of
  parameters.

- variables:

  Character vector of model parameter names. The output posterior
  summaries are restricted to these variables.

- summaries:

  List of summary functions passed to `...` in
  [`posterior::summarize_draws()`](https://mc-stan.org/posterior/reference/draws_summary.html)
  through `$summary()` on the `CmdStanFit` object.

- summary_args:

  List of summary function arguments passed to `.args` in
  [`posterior::summarize_draws()`](https://mc-stan.org/posterior/reference/draws_summary.html)
  through `$summary()` on the `CmdStanFit` object.

- transform:

  Symbol or `NULL`, name of a function that accepts arguments `data` and
  `draws` and returns a data frame. Here, `data` is the JAGS data list
  supplied to the model, and `draws` is a data frame with one column per
  model parameter and one row per posterior sample. Any arguments other
  than `data` and `draws` must have valid default values because
  `jagstargets` will not populate them. See the simulation-based
  calibration discussion thread at
  <https://github.com/ropensci/jagstargets/discussions/31> for an
  example.

## Value

A data frame of `R2jags` output. Depends on the `output` argument.
