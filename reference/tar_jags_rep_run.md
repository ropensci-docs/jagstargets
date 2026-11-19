# Run a batch of iterations for a jags model and return only strategic output.

Not a user-side function. Do not invoke directly.

## Usage

``` r
tar_jags_rep_run(
  jags_lines,
  jags_name,
  jags_file,
  parameters.to.save,
  data,
  variables = NULL,
  summaries = NULL,
  summary_args = NULL,
  transform = NULL,
  reps,
  output,
  n.cluster = n.cluster,
  n.chains = n.chains,
  n.iter = n.iter,
  n.burnin = n.burnin,
  n.thin = n.thin,
  jags.module = jags.module,
  inits = inits,
  RNGname = RNGname,
  stdout = stdout,
  stderr = stderr,
  progress.bar = progress.bar,
  refresh = refresh
)
```

## Arguments

- jags_lines:

  Character vector of lines from a JAGS file.

- jags_name:

  Friendly suffix of the jags model target.

- jags_file:

  Original path to the input jags file.

- parameters.to.save:

  Model parameters to save, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- data:

  A list, the original JAGS dataset.

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

- output:

  Character of length 1 denoting the type of output `tibble` to return:
  `"draws"` for MCMC samples (which could take up a lot of space)
  `"summary"` for lightweight posterior summary statistics, and `"dic"`
  for the overall deviance information criterion and effective number of
  parameters.

- n.cluster:

  Number of parallel processes, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- n.chains:

  Number of MCMC chains, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- n.iter:

  Number if iterations (including warmup), passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- n.burnin:

  Number of warmup iterations, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- n.thin:

  Thinning interval, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- jags.module:

  Character vector of JAGS modules to load, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- inits:

  Initial values of model parameters, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- RNGname:

  Choice of random number generator, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- stdout:

  Character of length 1, file path to write the stdout stream of the
  model when it runs. Set to `NULL` to print to the console. Set to
  [`R.utils::nullfile()`](https://henrikbengtsson.github.io/R.utils/reference/nullfile.html)
  to suppress stdout. Does not apply to messages, warnings, or errors.

- stderr:

  Character of length 1, file path to write the stderr stream of the
  model when it runs. Set to `NULL` to print to the console. Set to
  [`R.utils::nullfile()`](https://henrikbengtsson.github.io/R.utils/reference/nullfile.html)
  to suppress stderr. Does not apply to messages, warnings, or errors.

- progress.bar:

  Type of progress bar, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- refresh:

  Frequency for refreshing the progress bar, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

## Value

A data frame of posterior summaries.
