# extract_text

Extract text from a file

## Usage

``` r
extract_text(
  file,
  pages = NULL,
  area = NULL,
  password = NULL,
  encoding = NULL,
  copy = FALSE
)
```

## Arguments

- file:

  A character string specifying the path or URL to a PDF file.

- pages:

  An optional integer vector specifying pages to extract from.

- area:

  An optional list, of length equal to the number of pages specified,
  where each entry contains a four-element numeric vector of coordinates
  (top,left,bottom,right) containing the table for the corresponding
  page. As a convenience, a list of length 1 can be used to extract the
  same area from all (specified) pages.

- password:

  Optionally, a character string containing a user password to access a
  secured PDF.

- encoding:

  Optionally, a character string specifying an encoding for the text, to
  be passed to the assignment method of
  [`Encoding`](https://rdrr.io/r/base/Encoding.html).

- copy:

  Specifies whether the original local file(s) should be copied to
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html) before processing.
  `FALSE` by default. The argument is ignored if `file` is URL.

## Value

If `pages = NULL` (the default), a length 1 character vector, otherwise
a vector of length `length(pages)`.

## Details

This function converts the contents of a PDF file into a single
unstructured character string.

## See also

[`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md),
[`extract_areas`](https://docs.ropensci.org/tabulapdf/reference/extract_areas.md),
[`split_pdf`](https://docs.ropensci.org/tabulapdf/reference/split_merge.md)

## Author

Thomas J. Leeper \<thosjleeper@gmail.com\>

## Examples

``` r
# simple demo file
f <- system.file("examples", "fortytwo.pdf", package = "tabulapdf")

# extract all text
extract_text(f)
#> [1] "42 is the number from which the meaning of life, the universe, and everything can be derived.\n42 is the number from which the meaning of life, the universe, and everything can be derived.\n"

# extract all text from page 1 only
extract_text(f, pages = 1)
#> [1] "42 is the number from which the meaning of life, the universe, and everything can be derived.\n"

# extract text from selected area only
extract_text(f, area = list(c(209.4, 140.5, 304.2, 500.8)))
#> [1] "\n" "\n"
```
