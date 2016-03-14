FROM docker.io/jangorecki/r-pkg

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

# install R suggested dependencies
RUN Rscript -e 'install.packages(c("chron", "ggplot2", "plyr", "reshape", "reshape2", "testthat", "hexbin", "fastmatch", "nlme", "xts", "bit64", "gdata", "caret", "knitr", "curl", "zoo", "plm", "rmarkdown"))'

# install GenomicRanges from bioc
RUN Rscript -e 'source("https://bioconductor.org/biocLite.R"); biocLite("GenomicRanges")'

# start R
CMD ["R"]
