# Split and merge PDFs

Split PDF into separate pages or merge multiple PDFs into one.

## Usage

``` r
split_pdf(file, outdir = NULL, password = NULL, copy = FALSE)

merge_pdfs(file, outfile, copy = FALSE)
```

## Arguments

- file:

  For `merge_pdfs`, a character vector specifying the path to one or
  more *local* PDF files. For `split_pdf`, a character string specifying
  the path or URL to a PDF file.

- outdir:

  For `split_pdf`, an optional character string specifying a directory
  into which to split the resulting files. If `NULL`, the `outdir` is
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html). If `file` is a
  URL, both the original file and separate pages are stored in the R
  session's temporary directory.

- password:

  Optionally, a character string containing a user password to access a
  secured PDF. Currently, encrypted PDFs cannot be merged with
  `merge_pdfs`.

- copy:

  Specifies whether the original local file(s) should be copied to
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html) before processing.
  `FALSE` by default. The argument is ignored if `file` is URL.

- outfile:

  For `merge_pdfs`, a character string specifying the path to the PDF
  file to create from the merged documents.

## Value

For `split_pdfs`, a character vector specifying the output file names,
which are patterned after the value of `file`. For `merge_pdfs`, the
value of `outfile`.

## Details

`split_pdf` splits the file listed in `file` into separate one-page
doucments. `merge_pdfs` creates a single PDF document from multiple
separate PDF files.

## See also

[`extract_areas`](https://docs.ropensci.org/tabulapdf/reference/extract_areas.md),
[`get_page_dims`](https://docs.ropensci.org/tabulapdf/reference/get_page_dims.md),
[`make_thumbnails`](https://docs.ropensci.org/tabulapdf/reference/make_thumbnails.md)

## Author

Thomas J. Leeper \<thosjleeper@gmail.com\>

## Examples

``` r
# simple demo file
f <- system.file("examples", "mtcars.pdf", package = "tabulapdf")
get_n_pages(file = f)
#> [1] 3

# split PDF by page
sf <- split_pdf(f)

# merge pdf
mf <- file.path(tempdir(), "merged.pdf")
merge_pdfs(sf, mf)
#> [1] "/tmp/RtmpJrYCd5/merged.pdf"
get_n_pages(mf)
#> [1] 3
```
