# Calculates chlorpromazine-equivalent doses

Given a data.frame containing doses of antipsychotics to_cpz() converts
the doses into the equivalent chlorpromazine (CPZ) doses, using the
conversion factors specified in the key.

## Usage

``` r
to_cpz(
  input_data,
  ap_label,
  dose_label,
  route = "oral",
  key = chlorpromazineR::gardner2010,
  eq_label = "cpz_eq",
  factor_label = "cpz_conv_factor",
  route_label = NULL,
  q_label = NULL
)
```

## Arguments

- input_data:

  data.frame with antipsychotic name and dose data

- ap_label:

  column in x that stores antipsychotic name

- dose_label:

  column in x that stores dose

- route:

  options include "oral", "sai", "lai" or "mixed"

- key:

  source of the conversion factors–defaults to Gardner et al. 2010

- eq_label:

  the name of the column to be created, to save the calculated
  CPZ-equivalent dose

- factor_label:

  the name of the column to be created to store the conversion factors

- route_label:

  if "mixed" route is specified, provide the column that stores the
  route information

- q_label:

  if long-acting injectable doses are included, provide the column that
  stores the injection frequency (days), or only if the doses have
  already been divided, set q_label = 1.

## Value

data.frame with new variables storing conversion factor and
CPZ-equivalent doses

## Details

The default key is gardner2010 which has data for both oral and
long-acting antipsychotic medications. See help(gardner2010) for the
source reference.

## See also

Other conversion functions:
[`to_ap()`](https://docs.ropensci.org/chlorpromazineR/reference/to_ap.md)

## Examples

``` r
participant_ID <- c("P01", "P02", "P03", "P04")
age <- c(42, 29, 30, 60)
antipsychotic <- c("olanzapine", "olanzapine", "quetiapine", "ziprasidone")
dose <- c(10, 12.5, 300, 60)
example_oral <- data.frame(participant_ID, age, antipsychotic, dose, 
                           stringsAsFactors = FALSE)
to_cpz(example_oral, ap_label = "antipsychotic", dose_label = "dose", 
       route = "oral")
#>   participant_ID age antipsychotic  dose cpz_conv_factor cpz_eq
#> 1            P01  42    olanzapine  10.0           30.00    300
#> 2            P02  29    olanzapine  12.5           30.00    375
#> 3            P03  30    quetiapine 300.0            0.80    240
#> 4            P04  60   ziprasidone  60.0            3.75    225
```
