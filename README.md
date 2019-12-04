
# esc - Effect Size Computation for Meta Analysis <img src="man/figures/logo.png" align="right" />

[![DOI](https://zenodo.org/badge/62336116.svg)](https://zenodo.org/badge/latestdoi/62336116)

This is an R implementation of the web-based ‘Practical Meta-Analysis
Effect Size Calculator’ from David B. Wilson. The original calculator
can be found at
<http://www.campbellcollaboration.org/escalc/html/EffectSizeCalculator-Home.php>.

Based on the input, the effect size can be returned as standardized mean
difference (`d`), Cohen’s `f`, `eta` squared, Hedges’ `g`, correlation
coefficient effect size `r` or Fisher’s transformation `z`, odds ratio
or log odds effect size.

### Return values

The return value of all functions has the same structure:

  - The effect size, whether being `d`, `g`, `r`, `f`, (Cox) odds ratios
    or (Cox) logits, is always named `es`.
  - The standard error of the effect size, `se`.
  - The variance of the effect size, `var`.
  - The lower and upper confidence limits `ci.lo` and `ci.hi`.
  - The weight factor, based on the inverse-variance, `w`.
  - The total sample size `totaln`.
  - The effect size measure, `measure`, which is typically specified via
    the `es.type`-argument.
  - Information on the effect-size conversion, `info`.
  - A string with the study name, if the `study`-argument was specified
    in function calls.

#### Correlation Effect Size

If the correlation effect size `r` is computed, the transformed Fisher’s
z and their confidence intervals are also returned. The variance and
standard error for the correlation effect size r are always based on
Fisher’s transformation.

#### Odds Ratio Effect Size

For odds ratios, the variance and standard error are always returned on
the log-scale\!

### S3 methods

The **esc** package offers the S3 methods `print()` and
`as.data.frame()`.

### Combining results into a single data frame

The `combine_esc()` method is a convenient way to create pooled data
frames of different effect size calculations, for further use. Here is
an example of `combine_esc()`, which returns a `data.frame` object.

``` r
library(esc)
e1 <- esc_2x2(grp1yes = 30, grp1no = 50, grp2yes = 40, grp2no = 45, study = "Study 1")
e2 <- esc_2x2(grp1yes = 30, grp1no = 50, grp2yes = 40, grp2no = 45, es.type = "or", study = "Study 2")
e3 <- esc_t(p = 0.03, grp1n = 100, grp2n = 150, study = "Study 3")
e4 <- esc_mean_sd(grp1m = 7, grp1sd = 2, grp1n = 50, grp2m = 9, grp2sd = 3, grp2n = 60, es.type = "logit", 
    study = "Study 4")

combine_esc(e1, e2, e3, e4)
#>     study      es weight sample.size     se     var    ci.lo   ci.hi measure
#> 1 Study 1 -0.3930  9.945         165 0.3171 0.10056 -1.01456  0.2285   logit
#> 2 Study 2  0.6750  9.945         165 0.3171 0.10056  0.36256  1.2567      or
#> 3 Study 3  0.2818 59.434         250 0.1297 0.01683  0.02755  0.5360       d
#> 4 Study 4 -1.3982  7.721         110 0.3599 0.12951 -2.10354 -0.6928   logit
```

**esc** is still under development, i.e. not all effect size computation
options are implemented yet. The remaining options will follow in
further updates.

## Installation

### Latest development build

To install the latest development snapshot (see latest changes below),
type following commands into the R console:

``` r
library(githubinstall)
githubinstall::githubinstall("esc")
```

### Official, stable release

[![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/esc)](https://cran.r-project.org/package=esc)
  
[![downloads](http://cranlogs.r-pkg.org/badges/esc)](http://cranlogs.r-pkg.org/)
  
[![total](http://cranlogs.r-pkg.org/badges/grand-total/esc)](http://cranlogs.r-pkg.org/)

To install the latest stable release from CRAN, type following command
into the R console:

``` r
install.packages("esc")
```

## Citation

In case you want / have to cite my package, please use `citation('esc')`
for citation information.

[![DOI](https://zenodo.org/badge/62336116.svg)](https://zenodo.org/badge/latestdoi/62336116)
