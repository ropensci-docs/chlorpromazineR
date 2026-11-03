# Modify the names in a conversion key to only include the first word

For parenteral (sai) and long-acting/depot (lai) antipsychotics, the
name consists of the usual generic name (such as haloperidol) and a
second word describing the formulation (e.g. haloperidol decanoate).
Since to_cpz() and add_key() require exact matches to work properly,
removing the second word may be required, but should be done with care
as it can add ambiguity (e.g. fluphenazine enanthate and decanoate).

## Usage

``` r
trim_key(key)
```

## Arguments

- key:

  the key to trim

## Value

the key that was trimmed (a named list of 3 named lists)

## See also

Other key functions:
[`add_key()`](https://docs.ropensci.org/chlorpromazineR/reference/add_key.md),
[`check_key()`](https://docs.ropensci.org/chlorpromazineR/reference/check_key.md)

## Examples

``` r
trim_key(gardner2010)
#> The trim_key() function can introduce errors if used in improper
#>            circumstances. Ensure that the antipsychotic compounds in your data
#>            and in the intended keys are the same compounds. The trim function is
#>            for convenience, but would introduce errors in your data if the
#>            compounds are not equivalent.
#> $oral
#> $oral$chlorpromazine
#> [1] 1
#> 
#> $oral$amisulpride
#> [1] 0.8571429
#> 
#> $oral$aripiprazole
#> [1] 20
#> 
#> $oral$benperidol
#> [1] 120
#> 
#> $oral$clopenthixol
#> [1] 10
#> 
#> $oral$clorprothixene
#> [1] 1.2
#> 
#> $oral$clotiapine
#> [1] 6
#> 
#> $oral$clozapine
#> [1] 1.5
#> 
#> $oral$droperidol
#> [1] 60
#> 
#> $oral$flupenthixol
#> [1] 60
#> 
#> $oral$fluphenazine
#> [1] 50
#> 
#> $oral$haloperidol
#> [1] 60
#> 
#> $oral$levomepromazine
#> [1] 1.5
#> 
#> $oral$loxapine
#> [1] 10
#> 
#> $oral$mesoridazine
#> [1] 2
#> 
#> $oral$methotrimeprazine
#> [1] 2
#> 
#> $oral$molindone
#> [1] 6
#> 
#> $oral$olanzapine
#> [1] 30
#> 
#> $oral$oxypertine
#> [1] 2.5
#> 
#> $oral$paliperidone
#> [1] 66.66667
#> 
#> $oral$pericyazine
#> [1] 12
#> 
#> $oral$perphenazine
#> [1] 20
#> 
#> $oral$pimozide
#> [1] 75
#> 
#> $oral$prochlorperazine
#> [1] 6.818182
#> 
#> $oral$quetiapine
#> [1] 0.8
#> 
#> $oral$remoxipride
#> [1] 2.830189
#> 
#> $oral$risperidone
#> [1] 100
#> 
#> $oral$sertindole
#> [1] 30
#> 
#> $oral$sulpiride
#> [1] 0.75
#> 
#> $oral$thioridazine
#> [1] 1.2
#> 
#> $oral$thiothixene
#> [1] 20
#> 
#> $oral$trifluoperazine
#> [1] 30
#> 
#> $oral$trifluperidol
#> [1] 300
#> 
#> $oral$triflupromazine
#> [1] 6
#> 
#> $oral$ziprasidone
#> [1] 3.75
#> 
#> $oral$zotepine
#> [1] 2
#> 
#> $oral$zuclopenthixol
#> [1] 12
#> 
#> 
#> $sai
#> named list()
#> 
#> $lai
#> $lai$clopenthixol
#> [1] 28
#> 
#> $lai$flupenthixol
#> [1] 210
#> 
#> $lai$fluphenazine
#> [1] 336
#> 
#> $lai$fluphenazine
#> [1] 336
#> 
#> $lai$fluspirilene
#> [1] 700
#> 
#> $lai$haloperidol
#> [1] 112
#> 
#> $lai$perphenazine
#> [1] 84
#> 
#> $lai$pipotiazine
#> [1] 168
#> 
#> $lai$risperidone
#> [1] 168
#> 
#> $lai$zuclopenthixol
#> [1] 42
#> 
#> 
```
