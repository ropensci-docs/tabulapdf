# make_thumbnails

Convert Pages to Image Thumbnails

## Usage

``` r
make_thumbnails(
  file,
  outdir = NULL,
  pages = NULL,
  format = c("png", "jpeg", "bmp", "gif"),
  resolution = 72,
  password = NULL,
  copy = FALSE
)
```

## Arguments

- file:

  A character string specifying the path or URL to a PDF file.

- outdir:

  An optional character string specifying a directory into which to
  split the resulting files. If `NULL`, the `outdir` is
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html). If `file` is a
  URL, both file and thumbnails are stored in the R session's temporary
  directory.

- pages:

  An optional integer vector specifying pages to extract from.

- format:

  A character string specifying an image file format.

- resolution:

  A numeric value specifying the image resolution in DPI.

- password:

  Optionally, a character string containing a user password to access a
  secured PDF.

- copy:

  Specifies whether the original local file(s) should be copied to
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html) before processing.
  `FALSE` by default. The argument is ignored if `file` is URL.

## Value

A character vector of file paths.

## Details

This function save each (specified) page of a document as an image with
720 dpi resolution. Images are saved in the same directory as the
original file, with file names specified by the original file name, a
page number, and the corresponding file format extension.

## Note

This may generate Java “INFO” messages in the console, which can be
safely ignored.

## References

[Tabula](https://tabula.technology/)

## See also

[`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md),
[`extract_text`](https://docs.ropensci.org/tabulapdf/reference/extract_text.md),
`make_thumbnails`

## Author

Thomas J. Leeper \<thosjleeper@gmail.com\>

## Examples

``` r
# simple demo file
f <- system.file("examples", "mtcars.pdf", package = "tabulapdf")

make_thumbnails(f)
#> [1] "/tmp/RtmpJrYCd5/mtcars1.png" "/tmp/RtmpJrYCd5/mtcars2.png"
#> [3] "/tmp/RtmpJrYCd5/mtcars3.png"
```
