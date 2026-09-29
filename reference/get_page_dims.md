# Page length and dimensions

Get Page Length and Dimensions

## Usage

``` r
get_page_dims(file, doc, pages = NULL, password = NULL, copy = FALSE)

get_n_pages(file, doc, password = NULL, copy = FALSE)
```

## Arguments

- file:

  A character string specifying the path or URL to a PDF file.

- doc:

  Optionally,, in lieu of `file`, an rJava reference to a PDDocument
  Java object.

- pages:

  An optional integer vector specifying pages to extract from.

- password:

  Optionally, a character string containing a user password to access a
  secured PDF.

- copy:

  Specifies whether the original local file(s) should be copied to
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html) before processing.
  `FALSE` by default. The argument is ignored if `file` is URL.

## Value

For `get_n_pages`, an integer. For `get_page_dims`, a list of
two-element numeric vectors specifying the width and height of each
page, respectively.

## Details

`get_n_pages` returns the page length of a PDF document. `get_page_dims`
extracts the dimensions of specified pages in a PDF document. This can
be useful for figuring out how to specify the `area` argument in
[`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md)

## References

[Tabula](https://tabula.technology/)

## See also

[`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md),
[`extract_text`](https://docs.ropensci.org/tabulapdf/reference/extract_text.md),
[`make_thumbnails`](https://docs.ropensci.org/tabulapdf/reference/make_thumbnails.md)

## Author

Thomas J. Leeper \<thosjleeper@gmail.com\>

## Examples

``` r
# simple demo file
f <- system.file("examples", "mtcars.pdf", package = "tabulapdf")

get_n_pages(file = f)
#> [1] 3
get_page_dims(f)
#> [[1]]
#> [1] 612 792
#> 
#> [[2]]
#> [1] 612 792
#> 
#> [[3]]
#> [1] 612 792
#> 
```
