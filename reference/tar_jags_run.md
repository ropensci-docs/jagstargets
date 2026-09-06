# Run a JAGS model and return the whole output object.

Not a user-side function. Do not invoke directly.

## Usage

``` r
tar_jags_run(
  jags_lines,
  parameters.to.save,
  data,
  inits,
  n.cluster,
  n.chains,
  n.iter,
  n.burnin,
  n.thin,
  jags.module,
  RNGname,
  jags.seed,
  stdout,
  stderr,
  progress.bar,
  refresh
)
```

## Arguments

- jags_lines:

  Character vector of lines from a JAGS model file.

- parameters.to.save:

  Model parameters to save, passed to
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

- RNGname:

  Choice of random number generator, passed to
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) or
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html).
  See the argument documentation of the
  [`R2jags::jags()`](https://rdrr.io/pkg/R2jags/man/jags.html) and
  [`R2jags::jags.parallel()`](https://rdrr.io/pkg/R2jags/man/jags.html)
  help files for details.

- jags.seed:

  Seeds to apply to JAGS, passed to
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

An `R2jags` output object.
