# Write an example JAGS model file.

Overwrites the file at `path` with a built-in example JAGS model file.

## Usage

``` r
tar_jags_example_file(path = tempfile(pattern = "", fileext = ".jags"))
```

## Arguments

- path:

  Character of length 1, file path to write the model file.

## Value

`NULL` (invisibly).

## Examples

``` r
path <- tempfile(pattern = "", fileext = ".jags")
tar_jags_example_file(path = path)
writeLines(readLines(path))
#> model {
#>   for (i in 1:n) {
#>     y[i] ~ dnorm(x[i] * beta, 1)
#>   }
#>   beta ~ dnorm(0, 1)
#> }
```
