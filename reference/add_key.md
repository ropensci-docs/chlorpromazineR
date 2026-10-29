# Combine 2 keys with base key taking precedence

Use this to combine 2 keys by using the whole "base" key, and adding any
antipsychotics from the "added" key that are not in the "base" key.

## Usage

``` r
add_key(base, added, trim, verbose = TRUE)
```

## Arguments

- base:

  the base key

- added:

  the key from which other antipsychotics are found to add

- trim:

  TRUE to use trim_key on both the base and added key, needed when one
  does not use the full names (e.g. leucht2016).

- verbose:

  If TRUE, added antipsychotic names will be shown in a message

## Value

a merged key

## See also

Other key functions:
[`check_key()`](https://docs.ropensci.org/chlorpromazineR/reference/check_key.md),
[`trim_key()`](https://docs.ropensci.org/chlorpromazineR/reference/trim_key.md)

## Examples

``` r
add_key(gardner2010, leucht2016, trim = TRUE)
#> The trim_key() function can introduce errors if used in improper
#>            circumstances. Ensure that the antipsychotic compounds in your data
#>            and in the intended keys are the same compounds. The trim function is
#>            for convenience, but would introduce errors in your data if the
#>            compounds are not equivalent.
#> The trim_key() function can introduce errors if used in improper
#>            circumstances. Ensure that the antipsychotic compounds in your data
#>            and in the intended keys are the same compounds. The trim function is
#>            for convenience, but would introduce errors in your data if the
#>            compounds are not equivalent.
#> 24 (ORAL) were added to the base key (acepromazine, acetophenazine, asenapine, bromperidol, butaperazine, chlorprothixene, dixyrazine, flupentixol, levosulpiride, lurasidone, melperone, moperone, penfluridol, perazine, periciazine, pipamperone, pipotiazine, promazine, prothipendyl, sultopride, thiopropazate, thioproperazine, tiapride, tiotixene) 
#> 
#> 30 (SAI) were added to the base key (acepromazine, aripiprazole, bromperidol, chlorpromazine, chlorprothixene, clopenthixol, clotiapine, clozapine, dixyrazine, droperidol, haloperidol, levomepromazine, melperone, mesoridazine, moperone, olanzapine, perazine, periciazine, perphenazine, prochlorperazine, promazine, prothipendyl, remoxipride, sulpiride, thioproperazine, tiapride, trifluoperazine, triflupromazine, ziprasidone, zuclopenthixol) 
#> 
#> 4 (LAI) were added to the base key (bromperidol, flupentixol, olanzapine, paliperidone) 
#> 
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
#> $oral$acepromazine
#> [1] 3.0003
#> 
#> $oral$acetophenazine
#> [1] 5.9988
#> 
#> $oral$asenapine
#> [1] 14.9925
#> 
#> $oral$bromperidol
#> [1] 30.03003
#> 
#> $oral$butaperazine
#> [1] 30.03003
#> 
#> $oral$chlorprothixene
#> [1] 1
#> 
#> $oral$dixyrazine
#> [1] 5.9988
#> 
#> $oral$flupentixol
#> [1] 50
#> 
#> $oral$levosulpiride
#> [1] 0.7500188
#> 
#> $oral$lurasidone
#> [1] 5
#> 
#> $oral$melperone
#> [1] 1
#> 
#> $oral$moperone
#> [1] 14.9925
#> 
#> $oral$penfluridol
#> [1] 50
#> 
#> $oral$perazine
#> [1] 3.0003
#> 
#> $oral$periciazine
#> [1] 5.9988
#> 
#> $oral$pipamperone
#> [1] 1.499925
#> 
#> $oral$pipotiazine
#> [1] 30.03003
#> 
#> $oral$promazine
#> [1] 1
#> 
#> $oral$prothipendyl
#> [1] 1.25
#> 
#> $oral$sultopride
#> [1] 0.25
#> 
#> $oral$thiopropazate
#> [1] 5
#> 
#> $oral$thioproperazine
#> [1] 4
#> 
#> $oral$tiapride
#> [1] 0.7500188
#> 
#> $oral$tiotixene
#> [1] 10
#> 
#> 
#> $sai
#> $sai$acepromazine
#> [1] 5.9988
#> 
#> $sai$aripiprazole
#> [1] 20
#> 
#> $sai$bromperidol
#> [1] 30.03003
#> 
#> $sai$chlorpromazine
#> [1] 3.0003
#> 
#> $sai$chlorprothixene
#> [1] 5.9988
#> 
#> $sai$clopenthixol
#> [1] 3.0003
#> 
#> $sai$clotiapine
#> [1] 3.749531
#> 
#> $sai$clozapine
#> [1] 1
#> 
#> $sai$dixyrazine
#> [1] 10
#> 
#> $sai$droperidol
#> [1] 120.4819
#> 
#> $sai$haloperidol
#> [1] 37.45318
#> 
#> $sai$levomepromazine
#> [1] 3.0003
#> 
#> $sai$melperone
#> [1] 1
#> 
#> $sai$mesoridazine
#> [1] 1.499925
#> 
#> $sai$moperone
#> [1] 14.9925
#> 
#> $sai$olanzapine
#> [1] 30.03003
#> 
#> $sai$perazine
#> [1] 3.0003
#> 
#> $sai$periciazine
#> [1] 14.9925
#> 
#> $sai$perphenazine
#> [1] 30.03003
#> 
#> $sai$prochlorperazine
#> [1] 5.9988
#> 
#> $sai$promazine
#> [1] 3.0003
#> 
#> $sai$prothipendyl
#> [1] 1.25
#> 
#> $sai$remoxipride
#> [1] 1
#> 
#> $sai$sulpiride
#> [1] 0.3749953
#> 
#> $sai$thioproperazine
#> [1] 14.9925
#> 
#> $sai$tiapride
#> [1] 0.7500188
#> 
#> $sai$trifluoperazine
#> [1] 37.45318
#> 
#> $sai$triflupromazine
#> [1] 3.0003
#> 
#> $sai$ziprasidone
#> [1] 7.501875
#> 
#> $sai$zuclopenthixol
#> [1] 10
#> 
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
#> $lai$bromperidol
#> [1] 90.90909
#> 
#> $lai$flupentixol
#> [1] 75.18797
#> 
#> $lai$olanzapine
#> [1] 30.03003
#> 
#> $lai$paliperidone
#> [1] 120.4819
#> 
#> 
```
