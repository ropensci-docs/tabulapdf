# Changelog

## CHANGES TO tabulapdf 1.0.5-5

CRAN release: 2024-11-15

- Updated tests to use offline files.

## CHANGES TO tabulapdf 1.0.5-4

- Faster Shiny interface (parts of PR
  [\#56](https://github.com/ropensci/tabulapdf/issues/56),
  [@jkeuskamp](https://github.com/jkeuskamp))

## CHANGES TO tabulapdf 1.0.5-3

CRAN release: 2024-05-21

- CRAN release after the previous package was archived.

## CHANGES TO tabulapdf 1.0.5-2

- Uses readr for a much faster parsing of extracted tables.
- The default output format is now a list of tibbles.
- All tests pass.

## CHANGES TO tabulapdf 1.0.5

- Package renamed to `tabulapdf`
- New maintainer: [@pachadotdev](https://github.com/pachadotdev)
- Updated to use tabula-java 1.0.5
- Updated the methods in
  [`extract_tables()`](https://docs.ropensci.org/tabulapdf/reference/extract_tables.md)
- The version now follows the version of tabula-java
