# rJava logging

Toggle verbose rJava logging

## Usage

``` r
stop_logging()
```

## Value

`NULL`, invisibly.

## Details

This function turns off the somewhat verbose rJava logging, most of
which is uninformative. It is called automatically when tabulapdf is
attached via [`library()`](https://rdrr.io/r/base/library.html),
`require`, etc. To keep logging on, load the package namespace using
[`requireNamespace("tabulapdf")`](https://docs.ropensci.org/tabulapdf/)
and reference functions in using fully qualified references (e.g.,
[`tabulapdf::extract_tables()`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md).

## Note

This resets a global Java setting and may affect logging of other rJava
operations, requiring a restart of R.

## Author

Thomas J. Leeper \<thosjleeper@gmail.com\>

## Examples

``` r
stop_logging()
```
