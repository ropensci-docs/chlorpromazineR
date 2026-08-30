# Chlorpromazine equivalent key from Davis 1974 data

A list of antipsychotics and their chlorpromazine equivalent doses,
generated from the following file included with the package:
system.file("extdata", "davis1974.csv", package="chlorpromazineR").

## Usage

``` r
davis1974
```

## Format

A named list of 3 named lists (1 for each route) and each sub-list
contains the conversion factors for each antipsychotic. The 3 top-level
lists are named \`oral\`, \`sai\`, and \`lai\` (route), and the lists
they contain have names corresponding to the antipsychotic, e.g.
\`olanzapine\`.

## Source

John Davis (1974). Dose equivalence of the anti-psychotic drugs. Journal
of Psychiatric Research, 11, 65-69.
\<https://doi.org/10.1016/0022-3956(74)90071-5\>
