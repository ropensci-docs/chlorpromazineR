# Checks whether antipsychotic names are in the key

Provided a data.frame, x, this checks that the antipsychotic names
stored in the x's variable ap_label are present in the key.

## Usage

``` r
check_ap(
  input_data,
  key = chlorpromazineR::gardner2010,
  ap_label,
  route,
  route_label
)
```

## Arguments

- input_data:

  data.frame with antipsychotic name and dose data

- key:

  source of the conversion factors–defaults to Gardner et al. 2010

- ap_label:

  column in x that stores antipsychotic name

- route:

  options include "oral", "sai", "lai" or "mixed"

- route_label:

  if "mixed" route is specified, provide the column that stores the
  route information

## Value

number of antipsychotic names in x\[,ap_label\] that don't match key

## Examples

``` r
participant_ID <- c("P01", "P02", "P03", "P04")
age <- c(42, 29, 30, 60) # not used in calculation, just shows other data
                         # can exist in the data.frame
antipsychotic <- c("olanzapine", "olanzapine", "quetiapine", "ziprasidone")
dose <- c(10, 12.5, 300, 60)
example_oral <- data.frame(participant_ID, age, antipsychotic, dose, 
                           stringsAsFactors = FALSE)
check_ap(example_oral, ap_label = "antipsychotic", route = "oral", 
         key = gardner2010)
#> [1] 0
```
