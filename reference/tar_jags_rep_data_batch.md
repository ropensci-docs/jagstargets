# Generate a batch of data

Not a user-side function. Do not invoke directly.

## Usage

``` r
tar_jags_rep_data_batch(reps, batch, command)
```

## Arguments

- reps:

  Positive integer of length 1, number of reps to run.

- batch:

  Positive integer of length 1, index of the current batch.

- command:

  R code to run to generate one dataset.

## Value

A list of JAGS datasets containing data and dataset IDs.

## Examples

``` r
if (identical(Sys.getenv("TAR_JAGS_EXAMPLES"), "true")) {
tar_jags_rep_data_batch(2, 1, tar_jags_example_data())
}
```
