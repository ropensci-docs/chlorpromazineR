# Chlorpromazine equivalent key from Woods 2003 data

A list of antipsychotics and their chlorpromazine equivalent doses,
generated from the following file included with the package:
system.file("extdata", "woods2003.csv", package="chlorpromazineR").

## Usage

``` r
woods2003
```

## Format

A named list of 3 named lists (1 for each route) and each sub-list
contains the conversion factors for each antipsychotic. The 3 top-level
lists are named \`oral\`, \`sai\`, and \`lai\` (route), and the lists
they contain have names corresponding to the antipsychotic, e.g.
\`olanzapine\`.

## Source

Scott Woods (2003). Chlorpromazine Equivalent Doses for the Newer
Atypical Antipsychotics. Journal of Clinical Psychiatry. 64(6). 663-667.
\<https://doi.org/10.4088/JCP.v64n0607\>
