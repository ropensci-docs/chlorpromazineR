# Chlorpromazine equivalent key from Gardner et al. 2010 data

A list of antipsychotics and their chlorpromazine equivalent doses,
generated from the following file included with the package:
system.file("extdata", "gardner2010.csv", package="chlorpromazineR").

## Usage

``` r
gardner2010
```

## Format

A named list of 3 named lists (1 for each route) and each sub-list
contains the conversion factors for each antipsychotic. The 3 top-level
lists are named \`oral\`, \`sai\`, and \`lai\` (route), and the lists
they contain have names corresponding to the antipsychotic, e.g.
\`olanzapine\`.

## Source

Gardner, D. M., Murphy, A. L., O’Donnell, H., Centorrino, F., &
Baldessarini, R. J. (2010). International consensus study of
antipsychotic dosing. The American Journal of Psychiatry, 167(6),
686–693. \<https://doi.org/10.1176/appi.ajp.2009.09060802\>

## Details

The SAI data is not included in this key, because the original study did
not specify a conversion factor from chlorpromazine LAI to oral. The
alternative key gardner2010_withsai can be used, which includes the SAI
data, but the chlorpromazine equivalent doses produced are equivalent to
chlorpromazine SAI not chlorpromazine oral. They could be manually
converted (e.g. by multiplying the SAI doses by 3 per equivalence noted
by Davis 1974 \<https://doi.org/10.1016/0022-3956(74)90071-5\>)
