# Changelog

## jagstargets 1.2.3

- Add R-multiverse topic.

## jagstargets 1.2.2

CRAN release: 2024-11-18

- Use `qs2`.

## jagstargets 1.2.1

CRAN release: 2024-09-06

- Return `pV` instead of `pD` in DIC info
  ([\#35](https://github.com/ropensci/jagstargets/issues/35),
  [@giabaio](https://github.com/giabaio)).

## jagstargets 1.2.0

CRAN release: 2024-04-17

### Invalidating changes

- To align with <https://github.com/ropensci/targets/issues/1244> and
  <https://github.com/ropensci/targets/pull/1262>, switch the hashing
  functions from
  [`digest::digest()`](https://eddelbuettel.github.io/digest/man/digest.html)
  to
  [`secretbase::siphash13()`](https://shikokuchuo.net/secretbase/reference/siphash13.html).

### Other changes

- Add the new `description` arguments of
  [`tar_target()`](https://docs.ropensci.org/targets/reference/tar_target.html)
  (\`targets \>= 1.5.1.9001).
- Append model file information to the target descriptions using
  `tar_map()` (`tarchetypes` \>= 0.7.12.9001).

## jagstargets 1.1.0

CRAN release: 2023-01-06

- Add a `transform` argument to
  [`tar_jags_rep()`](https://docs.ropensci.org/jagstargets/reference/tar_jags_rep.md)
  to support simulation-based calibration.

## jagstargets 1.0.4

CRAN release: 2022-10-31

- Migrate docs away from deprecated
  [`targets::tar_path()`](https://docs.ropensci.org/targets/reference/tar_path.html).
- Implement resilient reps-specific seeds in the `tar_jags_rep*()`
  functions.

## jagstargets 1.0.3

CRAN release: 2022-06-24

- Append a new `.dataset_id` column to target outputs to aid in model
  comparisons across the same datasets.

## jagstargets 1.0.2

CRAN release: 2022-05-03

- Support the `repository` argument for `targets` \>= 0.11.0.

## jagstargets 1.0.1

CRAN release: 2021-12-03

- Adjust logo size for README.

## jagstargets 1.0.1

CRAN release: 2021-12-03

- Reference JOSS paper.

## jagstargets 1.0.0

- Add Zenodo and badge.
- Fix bibliography capitalization.

## jagstargets 0.0.1

- Complete rOpenSci review.
- Allow installation/checks to pass without `rjags` or `R2jags`
  installed ([\#18](https://github.com/ropensci/jagstargets/issues/18),
  [@jeroen](https://github.com/jeroen)).

## jagstargets 0.0.0.9002

- Replace the `log` argument with `stdout` and `stderr`.
- Switch meaning of `%||%` and `%|||%` to conform to historical
  precedent.

## jagstargets 0.0.0.9001

- Use `.join_data` list element instead of arguments `copy_data` and
  `omit_data`.

## jagstargets 0.0.0.9000

- Added a `NEWS.md` file to track changes to the package.
