
<!-- README.md is generated from README.Rmd. Please edit that file -->

# ggmsa: Plot multiple sequence alignment using ggplot2 <img src="man/figures/logo.png" height="139" align="right" />

<!-- badges: start -->

[![CRAN\_Release\_Badge](https://www.r-pkg.org/badges/version-ago/ggmsa)](https://cran.r-project.org/package=ggmsa)
[![CRAN\_Download\_Badge](https://cranlogs.r-pkg.org/badges/grand-total/ggmsa?color=green)](https://cran.r-project.org/package=ggmsa)
<!-- badges: end -->

`ggmsa` supports visualizing multiple sequence alignment of nucleotide
sequences and protein sequences using ggplot2. It supports a number of
colour schemes, including Chemistry, Clustal, Shapely, Taylor and Zappo.

## Install development version

The development version from github:

``` r
if (!requireNamespace("devtools", quietly=TRUE))
    install.packages("devtools")
devtools::install_github("YuLab-SMU/ggmsa")
```

## Quick Example

Plot multiple sequence alignment.

### Protein Sequences

``` r
library(ggmsa)
library(ggplot2)
protein_sequences <- system.file("extdata", "sample.fasta", package = "ggmsa")
ggmsa(protein_sequences, 164, 213, char_width = 0.5, color = "Chemistry_AA", seq_name = T)
```

![](man/figures/unnamed-chunk-3-1.png)<!-- -->

### DNA Sequences

``` r
nt_sequences <- system.file("extdata", "LeaderRepeat_All.fa", package = "ggmsa")
ggmsa(nt_sequences,font = NULL, color = "Chemistry_NT")
```

![](man/figures/unnamed-chunk-4-1.png)<!-- -->

### RNA Sequences

``` r
miRNA_sequences <- system.file("extdata", "seedSample.fa", package = "ggmsa")
ggmsa(miRNA_sequences, color = "Chemistry_NT")
```

![](man/figures/unnamed-chunk-5-1.png)<!-- -->

## Visualizing Multiple Sequence Alignment With `ggtree`.

``` r
library(Biostrings)
x <- readAAStringSet(protein_sequences)
d <- as.dist(stringDist(x, method = "hamming")/width(x)[1])
library(ape)
tree <- bionj(d)
library(ggtree)
p <- ggtree(tree) + geom_tiplab()

data = tidy_msa(x, 164, 213)
p + geom_facet(geom = geom_msa, data = data,  panel = 'msa',
               font = NULL, color = "Chemistry_AA") +
    xlim_tree(1)
```

![](man/figures/unnamed-chunk-6-1.png)<!-- -->

# Learn more

For more details about the version in CRAN, please refer to the [online
vignette](https://cran.r-project.org/web/packages/ggmsa/vignettes/ggmsa.html)

Moreover, check out the guides for learning new features with the
current development version:

  - [Getting
    Started](https://yulab-smu.github.io/ggmsa/articles/ggmsa.html)
  - [Extensions
    Plots](https://yulab-smu.github.io/ggmsa/articles/Extensions/extensions.html)
