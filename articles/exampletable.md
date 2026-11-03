# Examples produced by chlorpromazineR

``` r

library(chlorpromazineR)
```

For a walkthrough on this package’s functions and how to use them, see
the walkthrough vignette. The purpose of this vignette is to exhibit the
antipsychotics included by the conversion keys and their dose
equivalents.

## Gardner 2010

For the reference, see
[`help(gardner2010)`](https://docs.ropensci.org/chlorpromazineR/reference/gardner2010.md).

``` r

data_gardner_oral_names <- c("Amisulpride", "Aripiprazole", "Benperidol", "Chlorpromazine",
                             "Clopenthixol", "Clorprothixene", "Clotiapine", "Clozapine",
                             "Droperidol", "Flupenthixol", "Fluphenazine", "Haloperidol",
                             "Levomepromazine", "Loxapine", "Mesoridazine", 
                             "Methotrimeprazine", "Molindone", "Olanzapine", "Oxypertine",
                             "Paliperidone", "Pericyazine", "Perphenazine", "Pimozide",
                             "Prochlorperazine", "Quetiapine", "Remoxipride", "Risperidone",
                             "Sertindole", "Sulpiride", "Thioridazine", "Thiothixene",
                             "Trifluoperazine", "Trifluperidol", "Triflupromazine",
                             "Ziprasidone", "Zotepine", "Zuclopenthixol")

data_gardner_oral_median <- c(700, 30, 5, 600, 60, 500, 100, 400, 10, 10, 12, 10, 400, 
                              60, 300, 300, 100, 20, 240, 9, 50, 30, 8, 88, 750, 212, 6, 
                              20, 800, 500, 30, 20, 2, 100, 160, 300, 50)

data_gardner_oral <- data.frame(ap = data_gardner_oral_names, 
                                dose = data_gardner_oral_median)
```

## Oral route

### Equivalent to olanzapine 20 mg (CPZ 600 mg)

``` r

to_ap(data_gardner_oral, convert_to_ap = "olanzapine", ap_label = "ap", 
      dose_label = "dose", route = "oral")
#>                   ap dose cpz_conv_factor cpz_eq ap_eq
#> 1        amisulpride  700       0.8571429    600    20
#> 2       aripiprazole   30      20.0000000    600    20
#> 3         benperidol    5     120.0000000    600    20
#> 4     chlorpromazine  600       1.0000000    600    20
#> 5       clopenthixol   60      10.0000000    600    20
#> 6     clorprothixene  500       1.2000000    600    20
#> 7         clotiapine  100       6.0000000    600    20
#> 8          clozapine  400       1.5000000    600    20
#> 9         droperidol   10      60.0000000    600    20
#> 10      flupenthixol   10      60.0000000    600    20
#> 11      fluphenazine   12      50.0000000    600    20
#> 12       haloperidol   10      60.0000000    600    20
#> 13   levomepromazine  400       1.5000000    600    20
#> 14          loxapine   60      10.0000000    600    20
#> 15      mesoridazine  300       2.0000000    600    20
#> 16 methotrimeprazine  300       2.0000000    600    20
#> 17         molindone  100       6.0000000    600    20
#> 18        olanzapine   20      30.0000000    600    20
#> 19        oxypertine  240       2.5000000    600    20
#> 20      paliperidone    9      66.6666667    600    20
#> 21       pericyazine   50      12.0000000    600    20
#> 22      perphenazine   30      20.0000000    600    20
#> 23          pimozide    8      75.0000000    600    20
#> 24  prochlorperazine   88       6.8181818    600    20
#> 25        quetiapine  750       0.8000000    600    20
#> 26       remoxipride  212       2.8301887    600    20
#> 27       risperidone    6     100.0000000    600    20
#> 28        sertindole   20      30.0000000    600    20
#> 29         sulpiride  800       0.7500000    600    20
#> 30      thioridazine  500       1.2000000    600    20
#> 31       thiothixene   30      20.0000000    600    20
#> 32   trifluoperazine   20      30.0000000    600    20
#> 33     trifluperidol    2     300.0000000    600    20
#> 34   triflupromazine  100       6.0000000    600    20
#> 35       ziprasidone  160       3.7500000    600    20
#> 36          zotepine  300       2.0000000    600    20
#> 37    zuclopenthixol   50      12.0000000    600    20
```

### Equivalent to chlorpromazine 100 mg

``` r

data_gardner_oral_median_cpz100 <- data_gardner_oral_median / 6
data_gardner_oral_cpz100 <- data.frame(ap = data_gardner_oral_names,
                                       dose=data_gardner_oral_median_cpz100)

to_ap(data_gardner_oral_cpz100, convert_to_ap = "olanzapine", 
      ap_label = "ap", dose_label = "dose", route = "oral")
#>                   ap        dose cpz_conv_factor cpz_eq    ap_eq
#> 1        amisulpride 116.6666667       0.8571429    100 3.333333
#> 2       aripiprazole   5.0000000      20.0000000    100 3.333333
#> 3         benperidol   0.8333333     120.0000000    100 3.333333
#> 4     chlorpromazine 100.0000000       1.0000000    100 3.333333
#> 5       clopenthixol  10.0000000      10.0000000    100 3.333333
#> 6     clorprothixene  83.3333333       1.2000000    100 3.333333
#> 7         clotiapine  16.6666667       6.0000000    100 3.333333
#> 8          clozapine  66.6666667       1.5000000    100 3.333333
#> 9         droperidol   1.6666667      60.0000000    100 3.333333
#> 10      flupenthixol   1.6666667      60.0000000    100 3.333333
#> 11      fluphenazine   2.0000000      50.0000000    100 3.333333
#> 12       haloperidol   1.6666667      60.0000000    100 3.333333
#> 13   levomepromazine  66.6666667       1.5000000    100 3.333333
#> 14          loxapine  10.0000000      10.0000000    100 3.333333
#> 15      mesoridazine  50.0000000       2.0000000    100 3.333333
#> 16 methotrimeprazine  50.0000000       2.0000000    100 3.333333
#> 17         molindone  16.6666667       6.0000000    100 3.333333
#> 18        olanzapine   3.3333333      30.0000000    100 3.333333
#> 19        oxypertine  40.0000000       2.5000000    100 3.333333
#> 20      paliperidone   1.5000000      66.6666667    100 3.333333
#> 21       pericyazine   8.3333333      12.0000000    100 3.333333
#> 22      perphenazine   5.0000000      20.0000000    100 3.333333
#> 23          pimozide   1.3333333      75.0000000    100 3.333333
#> 24  prochlorperazine  14.6666667       6.8181818    100 3.333333
#> 25        quetiapine 125.0000000       0.8000000    100 3.333333
#> 26       remoxipride  35.3333333       2.8301887    100 3.333333
#> 27       risperidone   1.0000000     100.0000000    100 3.333333
#> 28        sertindole   3.3333333      30.0000000    100 3.333333
#> 29         sulpiride 133.3333333       0.7500000    100 3.333333
#> 30      thioridazine  83.3333333       1.2000000    100 3.333333
#> 31       thiothixene   5.0000000      20.0000000    100 3.333333
#> 32   trifluoperazine   3.3333333      30.0000000    100 3.333333
#> 33     trifluperidol   0.3333333     300.0000000    100 3.333333
#> 34   triflupromazine  16.6666667       6.0000000    100 3.333333
#> 35       ziprasidone  26.6666667       3.7500000    100 3.333333
#> 36          zotepine  50.0000000       2.0000000    100 3.333333
#> 37    zuclopenthixol   8.3333333      12.0000000    100 3.333333
```

## Short-acting injectables

``` r

data_gardner_sai_names <- c("Chlorpromazine HCl", "Clotiapine injectable",
                            "Fluphenazine HCl", "Haloperidol lactate",
                            "Loxapine HCl", "Mesoridazine besylate",
                            "Olanzapine tartrate", "Perphenazine USP",
                            "Prochlorperazine mesylate", "Promazine HCl",
                            "Trifluoperazine HCl", "Triflupromazine HCl",
                            "Ziprasidone mesylate", "Zuclopenthixol acetate")

data_gardner_sai_median <- c(100, 40, 5, 5, 25, 100, 10, 10, 22, 100, 
                             5, 60, 20, 50)

data_gardner_sai <- data.frame(ap = data_gardner_sai_names, 
                               dose = data_gardner_sai_median)


to_cpz(data_gardner_sai, key=gardner2010_withsai, ap_label = "ap", 
      dose_label = "dose", route = "sai")
#>                           ap dose cpz_conv_factor cpz_eq
#> 1         chlorpromazine hcl  100        1.000000    100
#> 2      clotiapine injectable   40        2.500000    100
#> 3           fluphenazine hcl    5       20.000000    100
#> 4        haloperidol lactate    5       20.000000    100
#> 5               loxapine hcl   25        4.000000    100
#> 6      mesoridazine besylate  100        1.000000    100
#> 7        olanzapine tartrate   10       10.000000    100
#> 8           perphenazine usp   10       10.000000    100
#> 9  prochlorperazine mesylate   22        4.545455    100
#> 10             promazine hcl  100        1.000000    100
#> 11       trifluoperazine hcl    5       20.000000    100
#> 12       triflupromazine hcl   60        1.666667    100
#> 13      ziprasidone mesylate   20        5.000000    100
#> 14    zuclopenthixol acetate   50        2.000000    100
```

### Equivalent to haloperidol 5 mg IM

``` r

to_ap(data_gardner_sai, key=gardner2010_withsai, 
      convert_to_ap = "haloperidol lactate", 
      ap_label = "ap", dose_label = "dose", route = "sai",
      convert_to_route = "sai")
#>                           ap dose cpz_conv_factor cpz_eq ap_eq
#> 1         chlorpromazine hcl  100        1.000000    100     5
#> 2      clotiapine injectable   40        2.500000    100     5
#> 3           fluphenazine hcl    5       20.000000    100     5
#> 4        haloperidol lactate    5       20.000000    100     5
#> 5               loxapine hcl   25        4.000000    100     5
#> 6      mesoridazine besylate  100        1.000000    100     5
#> 7        olanzapine tartrate   10       10.000000    100     5
#> 8           perphenazine usp   10       10.000000    100     5
#> 9  prochlorperazine mesylate   22        4.545455    100     5
#> 10             promazine hcl  100        1.000000    100     5
#> 11       trifluoperazine hcl    5       20.000000    100     5
#> 12       triflupromazine hcl   60        1.666667    100     5
#> 13      ziprasidone mesylate   20        5.000000    100     5
#> 14    zuclopenthixol acetate   50        2.000000    100     5
```

## Long-acting injectables

``` r

data_gardner_lai_names <- c("Clopenthixol decanoate", "Flupenthixol decanoate", 
                            "Fluphenazine decanoate", "Fluphenazine enanthate", 
                            "Fluspirilene", "Haloperidol decanoate", 
                            "Perphenazine enanthate", "Pipotiazine palmitate", 
                            "Risperidone microspheres", "Zuclopenthixol decanoate")

data_gardner_lai_median <- c(300, 40, 25, 25, 6, 150, 100, 100, 50, 200)

data_gardner_lai_q <- c(14, 14, 14, 14, 7, 28, 14, 28, 14, 14)

data_gardner_lai <- data.frame(ap = data_gardner_lai_names,
                               dose = data_gardner_lai_median,
                               q = data_gardner_lai_q)

to_cpz(data_gardner_lai, key=gardner2010, ap_label = "ap", 
       dose_label = "dose", route = "lai", q_label = "q")
#>                          ap dose  q cpz_conv_factor cpz_eq
#> 1    clopenthixol decanoate  300 14              28    600
#> 2    flupenthixol decanoate   40 14             210    600
#> 3    fluphenazine decanoate   25 14             336    600
#> 4    fluphenazine enanthate   25 14             336    600
#> 5              fluspirilene    6  7             700    600
#> 6     haloperidol decanoate  150 28             112    600
#> 7    perphenazine enanthate  100 14              84    600
#> 8     pipotiazine palmitate  100 28             168    600
#> 9  risperidone microspheres   50 14             168    600
#> 10 zuclopenthixol decanoate  200 14              42    600
```

## Davis 1974

For the reference, see
[`help(davis1974)`](https://docs.ropensci.org/chlorpromazineR/reference/davis1974.md).

``` r

data_davis_names <- c("Chlorpromazine", "Triflupromazine", "Thioridazine", "Prochlorperazine",
                      "Perphenazine", "Fluphenazine", "Trifluoperazine", "Acetophenazine", 
                      "Carphenazine", "Butaperazine", "Mesoridazine", "Piperacetazine", 
                      "Haloperidol", "Chlorprothixene", "Thiothixene")

data_davis_doses <- c(100, 28.4, 95.3, 14.3, 8.9, 1.2, 2.8, 23.5, 24.3, 8.9, 55.3, 10.5, 1.6, 
                     43.9, 5.2)

data_davis_oral <- data.frame(ap = data_davis_names, 
                              dose = data_davis_doses)
```

### Oral

``` r

to_cpz(data_davis_oral, ap_label = "ap", 
      dose_label = "dose", route = "oral", key=davis1974)
#>                  ap  dose cpz_conv_factor cpz_eq
#> 1    chlorpromazine 100.0        1.000000    100
#> 2   triflupromazine  28.4        3.521127    100
#> 3      thioridazine  95.3        1.049318    100
#> 4  prochlorperazine  14.3        6.993007    100
#> 5      perphenazine   8.9       11.235955    100
#> 6      fluphenazine   1.2       83.333333    100
#> 7   trifluoperazine   2.8       35.714286    100
#> 8    acetophenazine  23.5        4.255319    100
#> 9      carphenazine  24.3        4.115226    100
#> 10     butaperazine   8.9       11.235955    100
#> 11     mesoridazine  55.3        1.808318    100
#> 12   piperacetazine  10.5        9.523810    100
#> 13      haloperidol   1.6       62.500000    100
#> 14  chlorprothixene  43.9        2.277904    100
#> 15      thiothixene   5.2       19.230769    100
```

### Short acting injectable

The Davis ket converts parenteral (SAI) to oral chlorpromazine
equivalents on the basis of the statement in the text that oral is
assumed to be 3x the potency of oral.

``` r

to_cpz(data_davis_oral, ap_label = "ap", 
      dose_label = "dose", route = "sai", key=davis1974)
#>                  ap  dose cpz_conv_factor cpz_eq
#> 1    chlorpromazine 100.0        3.000000    300
#> 2   triflupromazine  28.4       10.563380    300
#> 3      thioridazine  95.3        3.147954    300
#> 4  prochlorperazine  14.3       20.979021    300
#> 5      perphenazine   8.9       33.707865    300
#> 6      fluphenazine   1.2      250.000000    300
#> 7   trifluoperazine   2.8      107.142857    300
#> 8    acetophenazine  23.5       12.765957    300
#> 9      carphenazine  24.3       12.345679    300
#> 10     butaperazine   8.9       33.707865    300
#> 11     mesoridazine  55.3        5.424955    300
#> 12   piperacetazine  10.5       28.571429    300
#> 13      haloperidol   1.6      187.500000    300
#> 14  chlorprothixene  43.9        6.833713    300
#> 15      thiothixene   5.2       57.692308    300
```

## Leucht 2016

For the reference, see
[`help(leucht2016)`](https://docs.ropensci.org/chlorpromazineR/reference/leucht2016.md).

``` r


leucht_names <- c("Acepromazine", "Acetophenazine", "Amisulpride", "Aripiprazole", 
                  "Asenapine", "Benperidol", "Bromperidol", "Butaperazine", "Cariprazine",
                  "Chlorproethazine", "Chlorpromazine", "Chlorprothixene", "Clopenthixol",
                  "Clotiapine", "Clozapine", "Cyamemazine", "Dixyrazine", "Droperidol",
                  "Fluanisone", "Flupentixol", "Fluphenazine", "Fluspirilene", "Haloperidol",
                  "Iloperidone", "Levomepromazine", "Levosulpiride", "Loxapine", "Lurasidone",
                  "Melperone", "Mesoridazine", "Molindone", "Moperone", "Mosapramine",
                  "Olanzapine", "Oxypertine", "Paliperidone", "Penfluridol", "Perazine",
                  "Periciazine", "Perphenazine", "Pimozide", "Pipamperone", "Pipotiazine",
                  "Prochlorperazine", "Promazine", "Prothipendyl", "Quetiapine", "Remoxipride",
                  "Risperidone", "Sertindole", "Sulpiride", "Sultopride", "Thiopropazate",
                  "Thioproperazine", "Thioridazine", "Tiapride", "Tiotixene", 
                  "Trifluoperazine", "Trifluperidol", "Triflupromazine", "Veralipride",
                  "Ziprasidone", "Zotepine", "Zuclopenthixol")

leucht_DDD_oral <- c(100, 50, 400, 15, 20, 1.5, 10, 10, NA, NA, 300, 300, 100, 80, 300, NA, 
                     50, NA, NA, 6, 10, NA, 8, NA, 300, 400, 100, 60, 300, 200, 50, 20, NA, 
                     10, 120, 6, 6, 100, 50, 30, 4, 200, 10, 100, 300, 240, 400, 300, 5, 16, 
                     800, 1200, 60, 75, 300, 400, 30, 20, 2, 100, NA, 80, 200, 30)

leucht_DDD_sai <- c(50, NA, NA, 15, NA, NA, 10, NA, NA, NA, 100, 50, 100, 80, 300, NA, 30, 
                    2.5, NA, NA, NA, NA, 8, NA, 100, NA, NA, NA, 300, 200, NA, 20, NA, 10, 
                    NA, NA, NA, 100, 20, 10, NA, NA, NA, 50, 100, 240, NA, 300, NA, NA, 
                    800, NA, NA, 20, NA, 400, NA, 8, NA, 100, NA, 40, NA, 30)

leucht_DDD_lai <- c(NA, NA, NA, NA, NA, NA, 3.3, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, 
                    NA, NA, 4, 1, 0.7, 3.3, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, 10.0, 
                    NA, 2.5, NA, NA, NA, 7.0, NA, NA, 5, NA, NA, NA, NA, NA, 2.7, NA, NA, 
                    NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, 15)



data_leucht_DDD_oral <- data.frame(ap = leucht_names, 
                              dose = leucht_DDD_oral)

data_leucht_DDD_sai <- data.frame(ap = leucht_names, 
                              dose = leucht_DDD_sai)

# pretend that all are given q 14 days
data_leucht_DDD_lai <- data.frame(ap = leucht_names, 
                                  dose = (leucht_DDD_lai*14), 
                                  q = rep(14, 64))

data_leucht_DDD_oral <- data_leucht_DDD_oral[!is.na(data_leucht_DDD_oral$dose),]
data_leucht_DDD_sai <- data_leucht_DDD_sai[!is.na(data_leucht_DDD_sai$dose),]
data_leucht_DDD_lai <- data_leucht_DDD_lai[!is.na(data_leucht_DDD_lai$dose),]


to_ap(data_leucht_DDD_oral, ap_label = "ap", dose_label = "dose", 
      route = "oral", key=leucht2016, convert_to_ap = "olanzapine")
#>                  ap   dose cpz_conv_factor   cpz_eq     ap_eq
#> 1      acepromazine  100.0       3.0003000 300.0300  9.990999
#> 2    acetophenazine   50.0       5.9988002 299.9400  9.988002
#> 3       amisulpride  400.0       0.7500188 300.0075  9.990250
#> 4      aripiprazole   15.0      20.0000000 300.0000  9.990000
#> 5         asenapine   20.0      14.9925037 299.8501  9.985007
#> 6        benperidol    1.5     200.0000000 300.0000  9.990000
#> 7       bromperidol   10.0      30.0300300 300.3003 10.000000
#> 8      butaperazine   10.0      30.0300300 300.3003 10.000000
#> 11   chlorpromazine  300.0       1.0000000 300.0000  9.990000
#> 12  chlorprothixene  300.0       1.0000000 300.0000  9.990000
#> 13     clopenthixol  100.0       3.0003000 300.0300  9.990999
#> 14       clotiapine   80.0       3.7495313 299.9625  9.988751
#> 15        clozapine  300.0       1.0000000 300.0000  9.990000
#> 17       dixyrazine   50.0       5.9988002 299.9400  9.988002
#> 20      flupentixol    6.0      50.0000000 300.0000  9.990000
#> 21     fluphenazine   10.0      30.0300300 300.3003 10.000000
#> 23      haloperidol    8.0      37.4531835 299.6255  9.977528
#> 25  levomepromazine  300.0       1.0000000 300.0000  9.990000
#> 26    levosulpiride  400.0       0.7500188 300.0075  9.990250
#> 27         loxapine  100.0       3.0003000 300.0300  9.990999
#> 28       lurasidone   60.0       5.0000000 300.0000  9.990000
#> 29        melperone  300.0       1.0000000 300.0000  9.990000
#> 30     mesoridazine  200.0       1.4999250 299.9850  9.989501
#> 31        molindone   50.0       5.9988002 299.9400  9.988002
#> 32         moperone   20.0      14.9925037 299.8501  9.985007
#> 34       olanzapine   10.0      30.0300300 300.3003 10.000000
#> 35       oxypertine  120.0       2.5000000 300.0000  9.990000
#> 36     paliperidone    6.0      50.0000000 300.0000  9.990000
#> 37      penfluridol    6.0      50.0000000 300.0000  9.990000
#> 38         perazine  100.0       3.0003000 300.0300  9.990999
#> 39      periciazine   50.0       5.9988002 299.9400  9.988002
#> 40     perphenazine   30.0      10.0000000 300.0000  9.990000
#> 41         pimozide    4.0      75.1879699 300.7519 10.015038
#> 42      pipamperone  200.0       1.4999250 299.9850  9.989501
#> 43      pipotiazine   10.0      30.0300300 300.3003 10.000000
#> 44 prochlorperazine  100.0       3.0003000 300.0300  9.990999
#> 45        promazine  300.0       1.0000000 300.0000  9.990000
#> 46     prothipendyl  240.0       1.2500000 300.0000  9.990000
#> 47       quetiapine  400.0       0.7500188 300.0075  9.990250
#> 48      remoxipride  300.0       1.0000000 300.0000  9.990000
#> 49      risperidone    5.0      59.8802395 299.4012  9.970060
#> 50       sertindole   16.0      18.7617261 300.1876  9.996248
#> 51        sulpiride  800.0       0.3749953 299.9963  9.989875
#> 52       sultopride 1200.0       0.2500000 300.0000  9.990000
#> 53    thiopropazate   60.0       5.0000000 300.0000  9.990000
#> 54  thioproperazine   75.0       4.0000000 300.0000  9.990000
#> 55     thioridazine  300.0       1.0000000 300.0000  9.990000
#> 56         tiapride  400.0       0.7500188 300.0075  9.990250
#> 57        tiotixene   30.0      10.0000000 300.0000  9.990000
#> 58  trifluoperazine   20.0      14.9925037 299.8501  9.985007
#> 59    trifluperidol    2.0     149.2537313 298.5075  9.940299
#> 60  triflupromazine  100.0       3.0003000 300.0300  9.990999
#> 62      ziprasidone   80.0       3.7495313 299.9625  9.988751
#> 63         zotepine  200.0       1.4999250 299.9850  9.989501
#> 64   zuclopenthixol   30.0      10.0000000 300.0000  9.990000

to_ap(data_leucht_DDD_sai, ap_label = "ap", dose_label = "dose", 
      route = "sai", key=leucht2016, convert_to_ap = "olanzapine", 
      convert_to_route = "sai")
#>                  ap  dose cpz_conv_factor   cpz_eq     ap_eq
#> 1      acepromazine  50.0       5.9988002 299.9400  9.988002
#> 4      aripiprazole  15.0      20.0000000 300.0000  9.990000
#> 7       bromperidol  10.0      30.0300300 300.3003 10.000000
#> 11   chlorpromazine 100.0       3.0003000 300.0300  9.990999
#> 12  chlorprothixene  50.0       5.9988002 299.9400  9.988002
#> 13     clopenthixol 100.0       3.0003000 300.0300  9.990999
#> 14       clotiapine  80.0       3.7495313 299.9625  9.988751
#> 15        clozapine 300.0       1.0000000 300.0000  9.990000
#> 17       dixyrazine  30.0      10.0000000 300.0000  9.990000
#> 18       droperidol   2.5     120.4819277 301.2048 10.030120
#> 23      haloperidol   8.0      37.4531835 299.6255  9.977528
#> 25  levomepromazine 100.0       3.0003000 300.0300  9.990999
#> 29        melperone 300.0       1.0000000 300.0000  9.990000
#> 30     mesoridazine 200.0       1.4999250 299.9850  9.989501
#> 32         moperone  20.0      14.9925037 299.8501  9.985007
#> 34       olanzapine  10.0      30.0300300 300.3003 10.000000
#> 38         perazine 100.0       3.0003000 300.0300  9.990999
#> 39      periciazine  20.0      14.9925037 299.8501  9.985007
#> 40     perphenazine  10.0      30.0300300 300.3003 10.000000
#> 44 prochlorperazine  50.0       5.9988002 299.9400  9.988002
#> 45        promazine 100.0       3.0003000 300.0300  9.990999
#> 46     prothipendyl 240.0       1.2500000 300.0000  9.990000
#> 48      remoxipride 300.0       1.0000000 300.0000  9.990000
#> 51        sulpiride 800.0       0.3749953 299.9963  9.989875
#> 54  thioproperazine  20.0      14.9925037 299.8501  9.985007
#> 56         tiapride 400.0       0.7500188 300.0075  9.990250
#> 58  trifluoperazine   8.0      37.4531835 299.6255  9.977528
#> 60  triflupromazine 100.0       3.0003000 300.0300  9.990999
#> 62      ziprasidone  40.0       7.5018755 300.0750  9.992498
#> 64   zuclopenthixol  30.0      10.0000000 300.0000  9.990000

to_ap(data_leucht_DDD_lai, ap_label = "ap", dose_label = "dose", 
      route = "lai", key=leucht2016, convert_to_ap = "olanzapine", q = "q")
#>                ap  dose  q cpz_conv_factor   cpz_eq    ap_eq
#> 7     bromperidol  46.2 14        90.90909 300.0000  9.99000
#> 20    flupentixol  56.0 14        75.18797 300.7519 10.01504
#> 21   fluphenazine  14.0 14       303.03030 303.0303 10.09091
#> 22   fluspirilene   9.8 14       434.78261 304.3478 10.13478
#> 23    haloperidol  46.2 14        90.90909 300.0000  9.99000
#> 34     olanzapine 140.0 14        30.03003 300.3003 10.00000
#> 36   paliperidone  35.0 14       120.48193 301.2048 10.03012
#> 40   perphenazine  98.0 14        42.91845 300.4292 10.00429
#> 43    pipotiazine  70.0 14        59.88024 299.4012  9.97006
#> 49    risperidone  37.8 14       111.11111 300.0000  9.99000
#> 64 zuclopenthixol 210.0 14        20.00000 300.0000  9.99000
```

## Woods 2003

For the reference, see
[`help(woods2003)`](https://docs.ropensci.org/chlorpromazineR/reference/woods2003.md).

``` r


woods_names <- c("haloperidol", "risperidone", "olanzapine",
                 "quetiapine", "ziprasidone", "aripiprazole")

woods_doses <- c(2, 2, 5, 75, 60, 7.5)

woods_oral <- data.frame(ap = woods_names, 
                         dose = woods_doses)

to_ap(woods_oral, route="oral", ap_label="ap", 
       dose="dose", key=woods2003, 
      convert_to_ap = "olanzapine")
#>             ap dose cpz_conv_factor cpz_eq ap_eq
#> 1  haloperidol  2.0       50.000000    100     5
#> 2  risperidone  2.0       50.000000    100     5
#> 3   olanzapine  5.0       20.000000    100     5
#> 4   quetiapine 75.0        1.333333    100     5
#> 5  ziprasidone 60.0        1.666667    100     5
#> 6 aripiprazole  7.5       13.333333    100     5
```
