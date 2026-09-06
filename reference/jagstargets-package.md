# jagstargets: Targets for JAGS Workflows

Bayesian data analysis usually incurs long runtimes and cumbersome
custom code. A pipeline toolkit tailored to Bayesian statisticians, the
`jagstargets` R package leverages `targets` and `R2jags` to ease this
burden. `jagstargets` makes it super easy to set up scalable JAGS
pipelines that automatically parallelize the computation and skip
expensive steps when the results are already up to date. Minimal custom
code is required, and there is no need to manually configure branching,
so usage is much easier than `targets` alone.

## See also

<https://docs.ropensci.org/jagstargets/>,
[`tar_jags()`](https://docs.ropensci.org/jagstargets/reference/tar_jags.md)
