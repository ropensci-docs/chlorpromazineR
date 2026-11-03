# Antipsychotic equivalent key from Leucht et al. 2020 data

A list of antipsychotics and their olanzapine-equivalent doses,
generated from the following file included with the package:
system.file("extdata", "leucht2020.csv", package="chlorpromazineR").

## Usage

``` r
leucht2020
```

## Format

A named list of 3 named lists (1 for each route) and each sub-list
contains the conversion factors for each antipsychotic. The 3 top-level
lists are named \`oral\`, \`sai\`, and \`lai\` (route), and the lists
they contain have names corresponding to the antipsychotic, e.g.
\`olanzapine\`.

## Source

Leucht, S., Crippa, A., Siafis, S., Patel, M., Orsini, N. & Davis, J. M.
(2020). Dose-Response Meta-Analysis of Antipsychotic Drugs for Acute
Schizophrenia. American Journal of Psychiatry. 117(4).
\<https://doi.org/10.1176/appi.ajp.2019.19010034\>

## Details

This reference does not include chlorpromazine, so the conversion from
leucht2016 is implied (i.e. chlorpromazine = olanzapine \* 30).
