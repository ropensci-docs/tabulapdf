# extract_tables

Extract tables from a file

## Usage

``` r
extract_tables(
  file,
  pages = NULL,
  area = NULL,
  columns = NULL,
  col_names = TRUE,
  guess = TRUE,
  method = c("decide", "lattice", "stream"),
  output = c("tibble", "matrix", "character", "asis", "csv", "tsv", "json"),
  outdir = NULL,
  password = NULL,
  encoding = NULL,
  copy = FALSE,
  ...
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
  same area from all (specified) pages. Only specify `area` or
  `columns`. Warning: `area` is ignored if `guess` is `TRUE`.

- columns:

  An optional list, of length equal to the number of pages specified,
  where each entry contains a numeric vector of horizontal (x)
  coordinates separating columns of data for the corresponding page. As
  a convenience, a list of length 1 can be used to specify the same
  columns for all (specified) pages. Only specify `area` or `columns`.
  Warning: `columns` is ignored if `guess` is `TRUE`.

- col_names:

  A logical indicating whether to include column names in the output
  tibbles. Default is `TRUE`.

- guess:

  A logical indicating whether to guess the locations of tables on each
  page. If `FALSE`, `area` or `columns` must be specified; if `TRUE`,
  `area` and `columns` are ignored.

- method:

  A string identifying the preferred method of table extraction.

  - `method = "decide"` (default) automatically decide (for each page)
    whether spreadsheet-like formatting is present and "lattice" is
    appropriate

  - `method = "lattice"` use Tabula's spreadsheet extraction algorithm

  - `method = "stream"` use Tabula's basic extraction algorithm

- output:

  A function to coerce the Java response object (a Java ArrayList of
  Tabula Tables) to some output format. The default method, “matrices”,
  returns a list of character matrices. See Details for other options.

- outdir:

  Output directory for files if `output` is set to `"csv"`, `"tsv"` or
  `"json"`, ignored otherwise. If equals `NULL` (default), uses R
  sessions temporary directory
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html).

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

- ...:

  These are additional arguments passed to the internal functions
  dispatched by `method`.

## Value

By default, a list of character matrices. This can be changed by
specifying an alternative value of `method` (see Details).

## Details

This function mimics the behavior of the Tabula command line utility. It
returns a list of R character matrices containing tables extracted from
a file by default. This response behavior can be changed by using the
following options.

- `output = "tibble"` attempts to coerce the structure returned by
  `method = "character"` into a list of tibbles and returns character
  strings where this fails.

- `output = "character"` returns a list of single-element character
  vectors, where each vector is a tab-delimited, line-separate string of
  concatenated table cells.

- `output = "csv"` writes the tables to comma-separated (CSV) files
  using Tabula's CSVWriter method in the same directory as the original
  PDF. `method = "tsv"` does the same but with tab-separated (TSV) files
  using Tabula's TSVWriter and `method = "json"` does the same using
  Tabula's JSONWriter method. Any of these three methods return the path
  to the directory containing the extract table files.

- `output = "asis"` returns the Java object reference, which can be
  useful for debugging or for writing a custom parser.

[`extract_areas`](https://docs.ropensci.org/tabulapdf/reference/extract_areas.md)
implements this functionality in an interactive mode allowing the user
to specify extraction areas for each page.

## References

[Tabula](https://tabula.technology/)

## See also

[`extract_areas`](https://docs.ropensci.org/tabulapdf/reference/extract_areas.md),
[`get_page_dims`](https://docs.ropensci.org/tabulapdf/reference/get_page_dims.md),
[`make_thumbnails`](https://docs.ropensci.org/tabulapdf/reference/make_thumbnails.md),
[`split_pdf`](https://docs.ropensci.org/tabulapdf/reference/split_merge.md)

## Author

Thomas J. Leeper \<thosjleeper@gmail.com\>, Tom Paskhalis
\<tpaskhalis@gmail.com\>

## Examples

``` r
# simple demo file
f <- system.file("examples", "mtcars.pdf", package = "tabulapdf")

# extract tables from only second page
extract_tables(f, pages = 2)
#> [[1]]
#> # A tibble: 1 × 5
#>   Sepal.Length                   Sepal.Width    Petal.Length Petal.Width Species
#>   <chr>                          <chr>          <chr>        <chr>       <chr>  
#> 1 "5.10\r4.90\r4.70\r4.60\r5.00" "3.50\r3.00\r… "1.40\r1.40… "0.20\r0.2… "setos…
#> 
```
