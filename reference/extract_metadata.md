# extract_metadata

Extract metadata from a file

## Usage

``` r
extract_metadata(file, password = NULL, copy = FALSE)
```

## Arguments

- file:

  A character string specifying the path or URL to a PDF file.

- password:

  Optionally, a character string containing a user password to access a
  secured PDF.

- copy:

  Specifies whether the original local file(s) should be copied to
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html) before processing.
  `FALSE` by default. The argument is ignored if `file` is URL.

## Value

A list.

## Details

This function extracts metadata from a PDF

## See also

[`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md),
[`extract_areas`](https://docs.ropensci.org/tabulapdf/reference/extract_areas.md),
[`extract_text`](https://docs.ropensci.org/tabulapdf/reference/extract_text.md),
[`split_pdf`](https://docs.ropensci.org/tabulapdf/reference/split_merge.md)

## Author

Thomas J. Leeper \<thosjleeper@gmail.com\>

## Examples

``` r
# simple demo file
f <- system.file("examples", "mtcars.pdf", package = "tabulapdf")

extract_metadata(f)
#> $pages
#> [1] 3
#> 
#> $title
#> NULL
#> 
#> $author
#> NULL
#> 
#> $subject
#> NULL
#> 
#> $keywords
#> NULL
#> 
#> $creator
#> [1] "LaTeX via pandoc"
#> 
#> $producer
#> [1] "xdvipdfmx (20240407)"
#> 
#> $created
#> [1] "Tue Apr 30 14:32:36 UTC 2024"
#> 
#> $modified
#> NULL
#> 
#> $trapped
#> NULL
#> 
```
