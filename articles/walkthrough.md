# Using chlorpromazineR to calculate chlorpromazine-equivalent doses

## Background

Studies investigating or controlling for the impact of antipsychotic
medications often need to quantify the amount of medication to which an
individual is or has been exposed. As different antipsychotics have
different potencies, the task is more complicated than using each
medication’s daily dosage in milligrams, for example. Further
complicating the matter is that antipsychotic medications have different
formulations including oral medications, and injectable formulations
that are either short- or long-acting (also called depots). A commonly
used strategy to account for the differing potencies is to calculate the
equivalent dose of each medication in terms of a reference medication.

Chlorpromazine (CPZ) is an antipsychotic medication most often used for
this purpose. A CPZ-equivalent dose is typically defined as a dose of
antipsychotic that is comparable to 100 mg of CPZ.[^1] The total daily
dose of a medication expressed in milligrams of CPZ per day is the
daily-dose equivalent, and is commonly utilized in both clinical and
research settings.[^2] Both strategies allow the dose of one medication,
such as quetiapine, to be expressed in equivalents of chlorpromazine.

There are various approaches to defining dose equivalents, including the
“defined daily doses” (Methodology WCCfDS, 2013), and Delphie
methods.[^3] Defined daily doses, which are produced by the World Health
Organization, provide an estimate of the average maintenance
antipsychotic daily dose required for a 70-kg adult with psychosis.[^4]
On the other hand, the Delphi method is an approach to reach a consensus
to antipsychotic dose equivalents based on a two-stage,
questionnaire-based survey of experts.[^5] Using the doses defined
through these methods, equivalency ratio for each antipsychotic can be
calculated, with CPZ as a reference medication (i.e. x mg/day of
antipsychotic A is equal to 1 mg/day CPZ).

While there is no single standard method to defining dose equivalence,
the International Consensus Study by Gardner et al. (2010), which used
the Delphi method,[^6] is a widely used resource to calculate
equivalency ratios.

## chlorpromazineR

We present here an easy-to-use R package to calculate CPZ daily dose
equivalents for common oral and injectable antipsychotic medications. We
do not propose to suggest which conversion factors are appropriate to
use, or how to interpret the converted data. All users should also refer
to the papers from which the conversion factor data originates to
determine whether the use of such data is appropriate for their study.

With this package, we hope:

- to improve transparency and consistency in calculating CPZ
  equivalents,
- to reduce human error and improve accuracy,
- and to simplify workflows for large datasets, as from chart reviews of
  electronic health records.

We use the data from the International Consensus Study (Gardner et
al. 2010) as the default conversion “key”. We also include keys
generated from the most widely cited papers on CPZ equivalence. The user
can also create their own keys (and contribute them to this package),
which are `list` objects as described below.

While the default key is `gardner2010`, derived from the 2010 paper by
Gardner et al, no equivalency was provided for short acting vs. oral
chlorpromazine, so `gardner2010` only includes oral and long acting
injectable conversion factors. However, the SAI equivalencies are
available in terms of chlorpromazine SAI equivalents, so to use that
data knowing this limitation, the key `gardner2010_withsai` is available
if needed. The SAI values calculated could then be converted using an
external reference value).

### Input data structure

The data is assumed to be stored in a `data.frame` where each row
represents a participant, and with the required variables stored in
columns. The two variables always required are the antipsychotic names
and the dose to convert. The generic name of the medication must be
used. There are differing conventions for drug name abbreviations, and
different brand names around the world, so brand names are not built
into the package.

For oral medications or short-acting injectables, the dose is converted
directly, i.e. not accounting for dosing frequencies, which must be done
separately. The exception is for long-acting injectables (LAIs), which
converts to daily equivalent oral CPZ dose by dividing by the frequency
of administration in days. Thus when using LAIs, a third variable, the
administration frequency in days, must be available, unless the stored
doses have already been divided by the administration frequency.

### Key data structure

The conversion factors are stored in “keys”. A key is a `list` object
containing 3 named sub-`lists`: `oral`, `sai` and `lai`.

``` r

names(gardner2010)
#> [1] "oral" "sai"  "lai"
```

Each sub-`list` is itself a named list where the names are the
antipsychotic names, and the values are the conversion factors.

``` r

names(gardner2010$oral)[1:5]
#> [1] "chlorpromazine" "amisulpride"    "aripiprazole"   "benperidol"    
#> [5] "clopenthixol"
```

The conversion factor is what a given dose needs to be multiplied by to
get the CPZ-equivalent.

``` r

gardner2010$oral$aripiprazole
#> [1] 20
```

For example, with aripiprazole, the value is 20, meaning that the
CPZ-equivalent dose of aripiprazole 5 mg is `5 * 20 = 100`.

## Tutorial

### Example for one route only

To demonstrate with a simple example using only oral medications,
consider the following data:

``` r

participant_ID <- c("P01", "P02", "P03", "P04")
age <- c(42, 29, 30, 60)
antipsychotic <- c("olanzapine", "olanzapine", "quetiapine", "ziprasidone")
dose <- c(10, 12.5, 300, 60)
example_oral <- data.frame(participant_ID, age, antipsychotic, dose, 
                           stringsAsFactors = FALSE)

example_oral
#>   participant_ID age antipsychotic  dose
#> 1            P01  42    olanzapine  10.0
#> 2            P02  29    olanzapine  12.5
#> 3            P03  30    quetiapine 300.0
#> 4            P04  60   ziprasidone  60.0
```

In this case we have `example_oral`, a `data.frame`, with one row per
participant, and a variable for the antipsychotic name, labeled
`antipsychotic` and a variable for the dose, named `dose`.

To calculate CPZ-equivalent doses, use the
[`to_cpz()`](https://docs.ropensci.org/chlorpromazineR/reference/to_cpz.md)
function:

``` r

to_cpz(example_oral, ap_label = "antipsychotic", dose_label = "dose", 
       route = "oral")
#>   participant_ID age antipsychotic  dose cpz_conv_factor cpz_eq
#> 1            P01  42    olanzapine  10.0           30.00    300
#> 2            P02  29    olanzapine  12.5           30.00    375
#> 3            P03  30    quetiapine 300.0            0.80    240
#> 4            P04  60   ziprasidone  60.0            3.75    225
```

Notice that 2 new columns appear, which are named based on the default
arguments in
[`to_cpz()`](https://docs.ropensci.org/chlorpromazineR/reference/to_cpz.md).
The CPZ-equivalent doses are in the column labeled `cpz_eq`.

### Example for data with oral and injectable routes

The default key from the study by Gardner et al. included dosing
equivalents for oral medications, short acting injectables and
long-acting injectables. If the original data includes more than one of
these routes, the `route` argument can be set to “mixed”.

In this case, more information is required to calculate the equivalent
doses. Specifically, a variable to indicate the route (“oral”, “sai”, or
“lai”) is required, and if long-acting injectables are used, then the
injection frequency is also required.\*

\*If the doses have already manually been divided by the frequency, then
setting the `q` parameter to `1` will forgo the need to specify a
variable storing the frequency information.

Here is some example data:

``` r

example_lai <- example_oral
example_lai$participant_ID <- c("P05", "P06", "P07", "P08")
example_lai$antipsychotic <- c("zuclopenthixol decanoate", 
                               "zuclopenthixol decanoate", 
                               "perphenazine enanthate", "fluspirilene")
example_lai$q <- c(14, 21, 14, 14)
example_lai$dose <- c(200, 200, 50, 6)

example_sai <- example_oral
example_sai$participant_ID <- c("P09", "P10", "P11", "P12")
example_sai$antipsychotic <- c("Chlorpromazine HCl", "Loxapine HCl", 
                               "Olanzapine tartrate", "Olanzapine tartrate")
example_sai$dose <- c(100, 50, 10, 5)

example_oral$q <- NA
example_sai$q <- NA

example_oral$route <- "oral"
example_lai$route <- "lai"
example_sai$route <- "sai"

example_mixed <- rbind(example_oral, example_sai, example_lai)

example_mixed
#>    participant_ID age            antipsychotic  dose  q route
#> 1             P01  42               olanzapine  10.0 NA  oral
#> 2             P02  29               olanzapine  12.5 NA  oral
#> 3             P03  30               quetiapine 300.0 NA  oral
#> 4             P04  60              ziprasidone  60.0 NA  oral
#> 5             P09  42       Chlorpromazine HCl 100.0 NA   sai
#> 6             P10  29             Loxapine HCl  50.0 NA   sai
#> 7             P11  30      Olanzapine tartrate  10.0 NA   sai
#> 8             P12  60      Olanzapine tartrate   5.0 NA   sai
#> 9             P05  42 zuclopenthixol decanoate 200.0 14   lai
#> 10            P06  29 zuclopenthixol decanoate 200.0 21   lai
#> 11            P07  30   perphenazine enanthate  50.0 14   lai
#> 12            P08  60             fluspirilene   6.0 14   lai
```

The function
[`to_cpz()`](https://docs.ropensci.org/chlorpromazineR/reference/to_cpz.md)
is used similarly as above, with the extra variable names (route_label,
q) specified:

``` r

to_cpz(example_mixed, ap_label = "antipsychotic", dose_label = "dose", 
       route = "mixed", route_label = "route", q_label = "q", key=gardner2010_withsai) 
#>    participant_ID age            antipsychotic  dose  q route cpz_conv_factor
#> 1             P01  42               olanzapine  10.0 NA  oral           30.00
#> 2             P02  29               olanzapine  12.5 NA  oral           30.00
#> 3             P03  30               quetiapine 300.0 NA  oral            0.80
#> 4             P04  60              ziprasidone  60.0 NA  oral            3.75
#> 5             P09  42       chlorpromazine hcl 100.0 NA   sai            1.00
#> 6             P10  29             loxapine hcl  50.0 NA   sai            4.00
#> 7             P11  30      olanzapine tartrate  10.0 NA   sai           10.00
#> 8             P12  60      olanzapine tartrate   5.0 NA   sai           10.00
#> 9             P05  42 zuclopenthixol decanoate 200.0 14   lai           42.00
#> 10            P06  29 zuclopenthixol decanoate 200.0 21   lai           42.00
#> 11            P07  30   perphenazine enanthate  50.0 14   lai           84.00
#> 12            P08  60             fluspirilene   6.0 14   lai          700.00
#>    cpz_eq
#> 1     300
#> 2     375
#> 3     240
#> 4     225
#> 5     100
#> 6     200
#> 7     100
#> 8      50
#> 9     600
#> 10    400
#> 11    300
#> 12    300
```

### Participants on multiple medications

If the included participants are on multiple medications, then the name
and dose of the antipsychotic should be specified as separate variables
in the `data.frame`. In this case,
[`to_cpz()`](https://docs.ropensci.org/chlorpromazineR/reference/to_cpz.md)
can be used multiple times, each time specifying the appropriate
variables. Run it first specifying the name and dose of the first
medication, and then run it again specifying the name and dose of the
second medication. Be sure to change the name of the `eq_label` where
the result will be stored.

## Checking for inclusion and matching of antipsychotic names

The software depends on an exact match (except for case) of the generic
names of antipsychotics. To check if there are rows that do not match,
[`check_ap()`](https://docs.ropensci.org/chlorpromazineR/reference/check_ap.md)
can be used. Here is an example of data where all the antipsychotic
names match the key, showing that 0 is returned (the number of
mismatches):

``` r

check_ap(example_oral, ap_label = "antipsychotic", route = "oral", key=gardner2010)
#> [1] 0
```

When there are mismatches, they are listed, and the number is returned:

``` r

example_sai <- example_sai
check_ap(example_sai, ap_label = "antipsychotic", route = "sai", key=gardner2010)
#> The following antipsychotics were not found in the key:
#> Chlorpromazine HCl (sai)
#> Loxapine HCl (sai)
#> Olanzapine tartrate (sai)
#> Olanzapine tartrate (sai)
#> [1] 4
```

As with
[`to_cpz()`](https://docs.ropensci.org/chlorpromazineR/reference/to_cpz.md),
mixed routes can be used with
[`check_ap()`](https://docs.ropensci.org/chlorpromazineR/reference/check_ap.md):

``` r

example_mixed_bad <- example_mixed
example_mixed_bad[1,3] <- "olanzzzzapine"
example_mixed_bad[4,3] <- "Seroquel"
example_mixed_bad[5,3] <- "chlorpromazineHCl"
example_mixed_bad[9,3] <- "zuclo decanoate"
check_ap(example_mixed_bad, ap_label = "antipsychotic", 
         route = "mixed", route_label = "route", key=gardner2010_withsai)
#> The following antipsychotics were not found in the key:
#> olanzzzzapine (oral)
#> Seroquel (oral)
#> chlorpromazineHCl (sai)
#> zuclo decanoate (lai)
#> [1] 4
```

While the default `gardner2010` key uses the full antipsychotic name for
SAI and LAI formulations (e.g. Chlorpromazine HCl) in order to be
consistent with the publication and reduce the risk of errors due to
ambiguity, the use can modify the key to “trim” the antipsychotic names
to just 1 word (e.g. chlorpromazine).

``` r

names(gardner2010$lai)
#>  [1] "clopenthixol decanoate"   "flupenthixol decanoate"  
#>  [3] "fluphenazine decanoate"   "fluphenazine enanthate"  
#>  [5] "fluspirilene"             "haloperidol decanoate"   
#>  [7] "perphenazine enanthate"   "pipotiazine palmitate"   
#>  [9] "risperidone microspheres" "zuclopenthixol decanoate"
```

To trim to 1-word antipsychotic names, we have made the
[`trim_key()`](https://docs.ropensci.org/chlorpromazineR/reference/trim_key.md)
function, which takes a key and generates a new key from it with the
1-word antipsychotic labels. If you want to use the `gardner2010` key
but want 1-word antipsychotic names, then you can use `trim_key` to
generate that new key, which you can then use in
[`to_cpz()`](https://docs.ropensci.org/chlorpromazineR/reference/to_cpz.md).
For example:

``` r

trimmed_gardner <- trim_key(gardner2010)
#> The trim_key() function can introduce errors if used in improper
#>            circumstances. Ensure that the antipsychotic compounds in your data
#>            and in the intended keys are the same compounds. The trim function is
#>            for convenience, but would introduce errors in your data if the
#>            compounds are not equivalent.

names(trimmed_gardner$lai)
#>  [1] "clopenthixol"   "flupenthixol"   "fluphenazine"   "fluphenazine"  
#>  [5] "fluspirilene"   "haloperidol"    "perphenazine"   "pipotiazine"   
#>  [9] "risperidone"    "zuclopenthixol"
```

## Using other keys

The above examples have used the default CPZ conversion key,
`gardner2010`, based on data extracted from Gardner et al. 2010.
However, not all antipsychotic medications were included in that study.
This package also includes a key extracted from the data included in the
Leucht et al. 2016 publication based on the World Health Organization’s
Defined Daily Doses. To explicitly change the CPZ key, use the key
parameter when calling
[`to_cpz()`](https://docs.ropensci.org/chlorpromazineR/reference/to_cpz.md).

``` r

to_cpz(example_oral, ap_label = "antipsychotic", dose_label = "dose", 
       route = "oral", key = leucht2016)
#>   participant_ID age antipsychotic  dose  q route cpz_conv_factor   cpz_eq
#> 1            P01  42    olanzapine  10.0 NA  oral      30.0300300 300.3003
#> 2            P02  29    olanzapine  12.5 NA  oral      30.0300300 375.3754
#> 3            P03  30    quetiapine 300.0 NA  oral       0.7500188 225.0056
#> 4            P04  60   ziprasidone  60.0 NA  oral       3.7495313 224.9719
```

However, the authors do not recommend using the DDD values when more
scientific values are available. Therefore, it can be desirable to
create a new key with data from the `gardner2010` key (or your own
created key) combined with the `leucht2016` key, using data from
`gardner2010` key where possible.

For this purpose, we have created the
[`add_key()`](https://docs.ropensci.org/chlorpromazineR/reference/add_key.md)
function, which takes a preferred base key from which ALL available
values are taken, and adds only the missing antipsychotic conversion
values from the second key to be added. Further, there is a `trim`
parameter, which invokes the
[`trim_key()`](https://docs.ropensci.org/chlorpromazineR/reference/trim_key.md)
function on both keys, in the case as in `leucht2016` where only 1-word
antipsychotic names are provided.

``` r

gardner_leucht <- add_key(base = gardner2010, add = leucht2016, trim = TRUE)
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

names(gardner_leucht$sai)
#>  [1] "acepromazine"     "aripiprazole"     "bromperidol"      "chlorpromazine"  
#>  [5] "chlorprothixene"  "clopenthixol"     "clotiapine"       "clozapine"       
#>  [9] "dixyrazine"       "droperidol"       "haloperidol"      "levomepromazine" 
#> [13] "melperone"        "mesoridazine"     "moperone"         "olanzapine"      
#> [17] "perazine"         "periciazine"      "perphenazine"     "prochlorperazine"
#> [21] "promazine"        "prothipendyl"     "remoxipride"      "sulpiride"       
#> [25] "thioproperazine"  "tiapride"         "trifluoperazine"  "triflupromazine" 
#> [29] "ziprasidone"      "zuclopenthixol"
```

Let’s change a value in the `example_oral` data so that there is an
antipsychotic that is not listed in the `gardner2010` key: asenapine.

``` r

other_oral <- example_oral
other_oral[2,3] <- "asenapine"
other_oral[2,4] <- 10

check_ap(other_oral, ap_label = "antipsychotic", route = "oral")
#> The following antipsychotics were not found in the key:
#> asenapine (oral)
#> [1] 1
```

We can see that asenapine is not in the default key. We could use the
`leucht2016` key:

``` r

to_cpz(other_oral, ap_label = "antipsychotic", dose_label = "dose", 
       route = "oral", key = gardner_leucht)
#>   participant_ID age antipsychotic dose  q route cpz_conv_factor  cpz_eq
#> 1            P01  42    olanzapine   10 NA  oral         30.0000 300.000
#> 2            P02  29     asenapine   10 NA  oral         14.9925 149.925
#> 3            P03  30    quetiapine  300 NA  oral          0.8000 240.000
#> 4            P04  60   ziprasidone   60 NA  oral          3.7500 225.000
```

Note that it used the `gardner2010` values where they were available
(olanzapine, quetiapine, ziprasidone) and the `leucht2016` key for
asenapine.

To draw from values from additional keys (e.g. user-created keys), the
[`add_key()`](https://docs.ropensci.org/chlorpromazineR/reference/add_key.md)
function could be used iteratively. The first argument of
[`add_key()`](https://docs.ropensci.org/chlorpromazineR/reference/add_key.md),
`base`, is always the key with values that take priority.

## List of included keys

Use the built in help function to see the full reference for any key,
e.g. [`help(davis1974)`](https://docs.ropensci.org/chlorpromazineR/reference/davis1974.md).
The data may need to be loaded prior to using the help function
(e.g. load via
[`chlorpromazineR::davis1974`](https://docs.ropensci.org/chlorpromazineR/reference/davis1974.md),
then use
[`help(davis1974)`](https://docs.ropensci.org/chlorpromazineR/reference/davis1974.md).

| Key name | Reference | Description |
|----|----|----|
| davis1974 | <https://doi.org/10.1016/0022-3956(74)90071-5> | Classic paper on chlorpromazine equivalent doses. |
| gardner2010 | <https://doi.org/10.1176/appi.ajp.2009.09060802> | Consensus study. |
| gardner2010_withsai | <https://doi.org/10.1176/appi.ajp.2009.09060802> | The included SAI data result in equivalent to SAI (parenteral) chlorpromazine, not oral. |
| leucht2016 | <https://doi.org/10.1093/schbul/sbv167> | WHO DDD method. |
| leucht2020 | <https://doi.org/10.1176/appi.ajp.2019.19010034> | Dose-response meta-analysis. |
| woods2003 | <https://doi.org/10.4088/JCP.v64n0607> |  |

## Converting to equivalents of an arbitrary antipsychotic

Historically, CPZ has been used as the reference antipsychotic. However,
using the same key data, any arbitrary reference antipsychotic could be
used. Similar to
[`to_cpz()`](https://docs.ropensci.org/chlorpromazineR/reference/to_cpz.md),
[`to_ap()`](https://docs.ropensci.org/chlorpromazineR/reference/to_ap.md)
can perform this conversion. The desired reference antipsychotic can be
specified, e.g. with the parameters
`convert_to_ap = "olanzapine", convert_to_route = "oral"`.

``` r

to_ap(other_oral, convert_to_ap = "olanzapine", convert_to_route = "oral", 
      ap_label = "antipsychotic", dose_label = "dose", 
      route = "oral", key = gardner_leucht)
#>   participant_ID age antipsychotic dose  q route cpz_conv_factor  cpz_eq
#> 1            P01  42    olanzapine   10 NA  oral         30.0000 300.000
#> 2            P02  29     asenapine   10 NA  oral         14.9925 149.925
#> 3            P03  30    quetiapine  300 NA  oral          0.8000 240.000
#> 4            P04  60   ziprasidone   60 NA  oral          3.7500 225.000
#>       ap_eq
#> 1 10.000000
#> 2  4.997501
#> 3  8.000000
#> 4  7.500000
```

[^1]: Davis, J. M. (1974). Dose equivalence of the antipsychotic drugs.
    Journal of Psychiatric Research, 1, 65–69.

[^2]: Danivas, V., & Venkatasubramanian, G. (2013). Current perspectives
    on chlorpromazine equivalents: Comparing apples and oranges! Indian
    Journal of Psychiatry, 55(2), 207–208.
    <https://doi.org/10.4103/0019-5545.111475>

[^3]: Dalkey, N. (1969). The Delphi Method: An Experimental Study of
    Group Opinion \| RAND. Retrieved from
    <https://www.rand.org/pubs/research_memoranda/RM5888.html>

[^4]: Leucht, S., Samara, M., Heres, S., & Davis, J. M. (2016). Dose
    Equivalents for Antipsychotic Drugs: The DDD Method. Schizophrenia
    Bulletin, 42(suppl_1), S90–S94.
    <https://doi.org/10.1093/schbul/sbv167>

[^5]: Hasson, F., Keeney, S., & McKenna, H. (2000). Research guidelines
    for the Delphi survey technique. Journal of Advanced Nursing, 32(4),
    1008–1015.

[^6]: Gardner, D. M., Murphy, A. L., O’Donnell, H., Centorrino, F., &
    Baldessarini, R. J. (2010). International consensus study of
    antipsychotic dosing. The American Journal of Psychiatry, 167(6),
    686–693. <https://doi.org/10.1176/appi.ajp.2009.09060802>
