Dockerfile for minimal setup of Ubuntu and R:
```
ubuntu + git + ssl + curl + vim + r-base-dev
```

And lightweight tools for R packages build, check, including Rmarkdown vignettes with knitr or rmarkdown:
```
qpdf + pandoc + knitr + rmarkdown + drat@artifacts
```

All suggested dependencies of data.table package
```r
c("chron", "ggplot2", "plyr", "reshape", "reshape2", "testthat", "hexbin", "fastmatch", "nlme", "xts", "bit64", "gdata", "caret", "knitr", "curl", "zoo", "plm", "rmarkdown","GenomicRanges")
```