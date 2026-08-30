# extract_areas

Interactively identify areas and extract

## Usage

``` r
locate_areas(
  file,
  pages = NULL,
  thumbnails = NULL,
  resolution = 60L,
  widget = c("shiny", "native", "reduced"),
  copy = FALSE
)

extract_areas(file, pages = NULL, guess = FALSE, copy = FALSE, ...)
```

## Arguments

- file:

  A character string specifying the path to a PDF file. This can also be
  a URL, in which case the file will be downloaded to the R temporary
  directory using `download.file`.

- pages:

  An optional integer vector specifying pages to extract from. To
  extract multiple tables from a given page, repeat the page number
  (e.g., `c(1,2,2,3)`).

- thumbnails:

  A directory containing prefetched thumbnails created with the function
  [`make_thumbnails`](https://docs.ropensci.org/tabulapdf/reference/make_thumbnails.md).
  This will greatly increase loading speed.

- resolution:

  An integer specifying the resolution of the PNG images conversions. A
  low resolution is used by default to speed image loading.

- widget:

  A one-element character vector specifying the type of “widget” to use
  for locating the areas. The default (“shiny”) is a shiny widget. The
  alternatives are a widget based on the native R graphics device
  (“native”, where available), or a very reduced functionality model
  (“reduced”).

- copy:

  Specifies whether the original local file(s) should be copied to
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html) before processing.
  `FALSE` by default. The argument is ignored if `file` is URL.

- guess:

  See
  [`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md)
  (note the different default value).

- ...:

  Other arguments passed to
  [`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md).

## Value

For `extract_areas`, see
[`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md).
For `locate_areas`, a list of four-element numeric vectors
(top,left,bottom,right), one per page of the file.

## Details

`extract_areas` is an interactive mode for
[`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md)
allowing the user to specify areas of each PDF page in a file that they
would like extracted. When used, each page is rendered to a PNG file and
displayed in an R graphics window sequentially, pausing on each page to
call [`locator`](https://rdrr.io/r/graphics/locator.html) so the user
can click and highlight an area to extract.

The exact behaviour is a somewhat platform-dependent, and depends on the
value of `widget` (and further, whether you are working in RStudio or
the R console). In RStudio (where `widget = "shiny"`), a Shiny gadget is
provided which allows the user to click and drag to select areas on each
page of a file, clicking “Done” on each page to advance through them. It
is not possible to return to previous pages. In the R console, a Shiny
app will be launched in a web browser.

For other values of `widget`, functionality is provided through the
graphics device. If graphics events are supported, then it is possibly
to interactively highlight a page region, make changes to that region,
and navigate through the pages of the document while retaining the area
highlighted on each page. If graphics events are not supported, then
some of this functionality is not available (see below).

In *full functionality mode* (`widget = "native"`), areas are input in a
native graphics device. For each page, the first mouse click on a page
initializes a highlighting rectangle; the second click confirms it. If
unsatisfied with the selection, the process can be repeated. The window
also responds to keystrokes. PgDn, Right, and Down advance to the next
page image, while PgUp, Left, and Up return to the previous page image.
Home returns to the first page image and End advances to the final page
image. Q quits the interactive mode and proceeds with extraction. When
navigating between pages, any selected areas will be displayed and can
be edited. Delete removes a highlighted area from a page (and then
displays it again). (This mode may not work correctly from within
RStudio.)

In *reduced functionality mode* (where `widget = "reduced"` or on
platforms where graphics events are unavailable), the interface requires
users to indicate the upper-left and lower-right (or upper-right and
lower-left) corners of an area on each page, this area will be briefly
confirmed with a highlighted rectangle and the next page will be
displayed. Dynamic page navigation and area editing are not possible.

In any of these modes, after the areas are selected, `extract_areas`
passes these user-defined areas to
[`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md).
`locate_areas` implements the interactive component only, without
actually extracting; this might be useful for interactive work that
needs some modification before executing `extract_tables`
computationally.

## See also

[`extract_tables`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md),
[`make_thumbnails`](https://docs.ropensci.org/tabulapdf/reference/make_thumbnails.md),
,
[`get_page_dims`](https://docs.ropensci.org/tabulapdf/reference/get_page_dims.md)

## Author

Thomas J. Leeper \<thosjleeper@gmail.com\>

## Examples

``` r
if (interactive()) {
  # simple demo file
  f <- system.file("examples", "mtcars.pdf", package = "tabulapdf")

  # locate areas only, using Shiny app
  locate_areas(f)

  # locate areas only, using native graphics device
  locate_areas(f, widget = "shiny")

  # locate areas and extract
  extract_areas(f)
}
```
