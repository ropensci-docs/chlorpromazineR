# Calculates equivalent doses

As in to_cpz(), to_ap() converts doses of antipsychotics into equivalent
doses to a reference antipsychotic. Whereas in to_cpz() the reference
antipsychotic is chlorpromazine (CPZ), to_ap() converts to equivalents
of an arbitrary antipsychotic specified as a string to convert_to_ap.
Conversion factors are specified in the key.

## Usage

``` r
to_ap(
  input_data,
  convert_to_ap = "olanzapine",
  convert_to_route = "oral",
  ap_label,
  dose_label,
  route = "oral",
  key = chlorpromazineR::gardner2010,
  cpz_eq_label = "cpz_eq",
  ref_eq_label = "ap_eq",
  factor_label = "cpz_conv_factor",
  route_label = NULL,
  q_label = NULL
)
```

## Arguments

- input_data:

  data.frame with antipsychotic name and dose data

- convert_to_ap:

  name of desired reference antipsychotic

- convert_to_route:

  the route of the desired reference antipsychotic

- ap_label:

  column in x that stores antipsychotic name

- dose_label:

  column in x that stores dose

- route:

  options include "oral", "sai", "lai" or "mixed"

- key:

  source of the conversion factors–defaults to Gardner et al. 2010

- cpz_eq_label:

  the name of the column to be created, to save the calculated
  CPZ-equivalent dose

- ref_eq_label:

  the name of the column to be created to save the doses in terms of the
  specified reference antipsychotic (in convert_to_ap)

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

## See also

Other conversion functions:
[`to_cpz()`](https://docs.ropensci.org/chlorpromazineR/reference/to_cpz.md)

## Examples

``` r
participant_ID <- c("P01", "P02", "P03", "P04")
age <- c(42, 29, 30, 60) # not used in calculation, just shows other data
                         # can exist in the data.frame
antipsychotic <- c("olanzapine", "olanzapine", "quetiapine", "ziprasidone")
dose <- c(10, 12.5, 300, 60)
example_oral <- data.frame(participant_ID, age, antipsychotic, dose,
                           stringsAsFactors = FALSE)
to_ap(example_oral, convert_to_ap="olanzapine", convert_to_route="oral",
      ap_label = "antipsychotic", dose_label = "dose", route = "oral")
#>   participant_ID age antipsychotic  dose cpz_conv_factor cpz_eq ap_eq
#> 1            P01  42    olanzapine  10.0           30.00    300  10.0
#> 2            P02  29    olanzapine  12.5           30.00    375  12.5
#> 3            P03  30    quetiapine 300.0            0.80    240   8.0
#> 4            P04  60   ziprasidone  60.0            3.75    225   7.5
```
