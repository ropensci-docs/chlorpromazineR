# Chlorpromazine equivalent key from Leucht et al. 2016 data

A list of antipsychotics and their chlorpromazine equivalent doses,
generated from the following file included with the package:
system.file("extdata", "leucht2016.csv", package="chlorpromazineR").

## Usage

``` r
leucht2016
```

## Format

A named list of 3 named lists (1 for each route) and each sub-list
contains the conversion factors for each antipsychotic. The 3 top-level
lists are named \`oral\`, \`sai\`, and \`lai\` (route), and the lists
they contain have names corresponding to the antipsychotic, e.g.
\`olanzapine\`.

## Source

Leucht, S., Samara, M., Heres, S., & Davis, J. M. (2016). Dose
Equivalents for Antipsychotic Drugs: The DDD Method. Schizophrenia
Bulletin, 42(suppl_1), S90–S94.
\<https://doi.org/10.1093/schbul/sbv167\>
