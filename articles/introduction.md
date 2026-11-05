# Introduction to jagstargets

The `jagstargets` package makes it easy to run a single jags model and
keep track of the results.
[`R2jags`](https://github.com/suyusung/R2jags) fits the models, and
[`targets`](https://docs.ropensci.org/targets/) manages the workflow and
helps avoid unnecessary computation.

Consider the simple regression model below with response variable `y`
and covariate `x`.

\\ \begin{aligned} y_i &\stackrel{\text{iid}}{\sim} \text{Normal}(x_i
\beta, 1) \\ \beta &\sim \text{Normal}(0, 1) \end{aligned} \\

We write this model in the JAGS model file below.

``` r

lines <- "model {
  for (i in 1:n) {
    y[i] ~ dnorm(x[i] * beta, 1)
  }
  beta ~ dnorm(0, 1)
}"
writeLines(lines, "x.jags")
```

A typical workflow proceeds as follows:

1.  Prepare a list of input data to JAGS, including vector elements `x`
    and `y`.
2.  Fit the JAGS model using the list of input data.
3.  Use the fitted model object to compute posterior summaries and
    convergence diagnostics.
4.  Use the fitted model object to extract posterior draws of parameters
    and store them in a tidy data frame.
5.  If there are other models to compare, use the fitted model object to
    compute the deviance information criterion (DIC).

`jagstargets` encapsulates this workflow with the
[`tar_jags()`](https://docs.ropensci.org/jagstargets/reference/tar_jags.html)
function. To use it in a [`targets`](https://docs.ropensci.org/targets/)
pipeline, invoke it from the `_targets.R` script of the project.

``` r

# _targets.R
library(targets)
library(jagstargets)

generate_data <- function(n = 10) {
  true_beta <- stats::rnorm(n = 1, mean = 0, sd = 1)
  x <- seq(from = -1, to = 1, length.out = n)
  y <- stats::rnorm(n, x * true_beta, 1)
  out <- list(n = n, x = x, y = y)
}

# The _targets.R file ends with a list of target objects
# produced by jagstargets::tar_jags(), targets::tar_target(), or similar.
list(
  tar_jags(
    example,
    jags_files = "x.jags",
    parameters.to.save = "beta",
    data = generate_data()
  )
)
```

[`tar_jags()`](https://docs.ropensci.org/jagstargets/reference/tar_jags.html)
only *defines* the pipeline. It does not actually run JAGS, it declares
the targets that will eventually run JAGS. The specific targets are as
follows. Run
[`tar_manifest()`](https://docs.ropensci.org/targets/reference/tar_manifest.html)
to show specific details about the targets declared.

``` r

tar_manifest()
```

Each target is responsible for a piece of the workflow.

- `example_file_x`: Reproducibly track changes to the jags model file.
- `example_data`: Run the code you supplied to the `data` argument of
  [`tar_jags()`](https://docs.ropensci.org/jagstargets/reference/tar_jags.md)
  and return a dataset compatible with JAGS.
- `example_mcmc_x`: Run the MCMC and return an object of class `rjags`
  from [`R2jags`](https://github.com/suyusung/R2jags).
- `example_draws_x`: Return a friendly `tibble` of the posterior draws
  from `example`.
- `example_summaries_x`: Return a friendly `tibble` of the posterior
  summaries from `example`. Uses
  [`posterior::summarize_draws()`](https://mc-stan.org/posterior/reference/draws_summary.html)
- `example_dic_x`: Return a friendly `tibble` with each model’s DIC and
  penalty.

The suffix `_x` comes from the base name of the model file, in this case
`x.jags`. If you supply multiple model files to the `jags_files`
argument, all the models share the same dataset, and the suffixes
distinguish among the various targets.

The targets depend on one another: for example, `example_mcmc_x` takes
`example_data` as input. [`targets`](https://docs.ropensci.org/targets/)
can visualize the dependency relationships in a dependency graph, which
is helpful for understanding the pipeline and troubleshooting issues.

``` r

tar_visnetwork(targets_only = TRUE)
```

Run the computation with
[`tar_make()`](https://docs.ropensci.org/targets/reference/tar_make.html).

``` r

tar_make()
```

The output lives in a special folder called `_targets/` and you can
retrieve it with functions
[`tar_load()`](https://docs.ropensci.org/targets/reference/tar_load.html)
and
[`tar_read()`](https://docs.ropensci.org/targets/reference/tar_read.html)
(from [`targets`](https://docs.ropensci.org/targets/)).

``` r

tar_read(example_summary_x)
```

At this point, all our results are up to date because their dependencies
did not change.

``` r

tar_make()
```

But if we change the underlying code or data, some of the targets will
no longer be valid, and they will rerun during the next
[`tar_make()`](https://docs.ropensci.org/targets/reference/tar_make.html).
Below, we change the jags model file, so the MCMC reruns while the data
is skipped. This behavior saves time and enhances reproducibility.

``` r

write(" ", file = "x.jags", append = TRUE)
```

``` r

tar_outdated()
```

``` r

tar_visnetwork(targets_only = TRUE)
```

``` r

tar_make()
```

At this point, we can add more targets and custom functions for
additional post-processing. See below for a custom summary target (which
is equivalent to customizing the `summaries` argument of
[`tar_jags()`](https://docs.ropensci.org/jagstargets/reference/tar_jags.md).)

``` r

# _targets.R
library(targets)
library(jagstargets)

generate_data <- function(n = 10) {
  true_beta <- stats::rnorm(n = 1, mean = 0, sd = 1)
  x <- seq(from = -1, to = 1, length.out = n)
  y <- stats::rnorm(n, x * true_beta, 1)
  out <- list(n = n, x = x, y = y)
}

list(
  tar_jags(
    example,
    jags_files = "x.jags",
    parameters.to.save = "beta",
    data = generate_data()
  ),
  tar_target(
    custom_summary,
    posterior::summarize_draws(
      dplyr::select(example_draws_x, -starts_with(".")),
      ~posterior::quantile2(.x, probs = c(0.25, 0.75))
    )
  )
)
```

In the graph, our new `custom_summary` target should be connected to the
upstream `example` target, and only `custom_summary` should be out of
date.

``` r

tar_visnetwork(targets_only = TRUE)
```

In the next
[`tar_make()`](https://docs.ropensci.org/targets/reference/tar_make.html),
we skip the expensive MCMC and just run the custom summary.

``` r

tar_make()
```

``` r

tar_read(custom_summary)
```

## Multiple models

[`tar_jags()`](https://docs.ropensci.org/jagstargets/reference/tar_jags.md)
and related functions allow you to supply multiple models to
`jags_files`. If you do, each model will run on the same dataset.
Consider a new model, `y.jags`.

``` r

lines <- "model {
  for (i in 1:n) {
    y[i] ~ dnorm(x[i] * x[i] * beta, 1) # Regress on x^2 instead of x.
  }
  beta ~ dnorm(0, 1)
}"
writeLines(lines, "y.jags")
```

Below, we add `y.jags` to the `jags_files` argument of
[`tar_jags()`](https://docs.ropensci.org/jagstargets/reference/tar_jags.md).

``` r

# _targets.R
library(targets)
library(jagstargets)

generate_data <- function(n = 10) {
  true_beta <- stats::rnorm(n = 1, mean = 0, sd = 1)
  x <- seq(from = -1, to = 1, length.out = n)
  y <- stats::rnorm(n, x * true_beta, 1)
  out <- list(n = n, x = x, y = y)
}

list(
  tar_jags(
    example,
    jags_files = c("x.jags", "y.jags"),
    parameters.to.save = "beta",
    data = generate_data()
  ),
  tar_target(
    custom_summary,
    posterior::summarize_draws(
      dplyr::select(example_draws_x, -starts_with(".")),
      ~posterior::quantile2(.x, probs = c(0.25, 0.75))
    )
  )
)
```

In the graph below, notice how the `*_x` targets and `*_y` targets are
both connected to `example_data` upstream.

``` r

tar_visnetwork(targets_only = TRUE)
```

## More information

For more on [`targets`](https://docs.ropensci.org/targets/), please
visit the reference website <https://docs.ropensci.org/targets/> or the
user manual <https://books.ropensci.org/targets/>. The manual walks
though advanced features of `targets` such as [high-performance
computing](https://books.ropensci.org/targets/hpc.html) and [cloud
storage
support](https://books.ropensci.org/targets/data.html#cloud-storage).
