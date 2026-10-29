# Check whether a conversion key is the expected format

chlorpromazineR uses conversion factors stored in a named list of 3
named lists. This verifies that the key is in a usable format, which can
be helpful when creating custom keys or modifying included keys.

## Usage

``` r
check_key(key)
```

## Arguments

- key:

  the key to check

## Value

TRUE if the key is valid, otherwise a error is thrown.

## See also

Other key functions:
[`add_key()`](https://docs.ropensci.org/chlorpromazineR/reference/add_key.md),
[`trim_key()`](https://docs.ropensci.org/chlorpromazineR/reference/trim_key.md)

## Examples

``` r
check_key(gardner2010)
#> [1] TRUE
```
