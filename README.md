Dockefiles:  
  - `drd-pkg`: extends `docker.io/rocker-org/drd` for building Rmd vignettes with knitr or rmarkdown.  
  - `r-base-dev`: extends `ubuntu:14.04` for r-base-dev.  
  - `r-pkg`: extends `r-base-dev` for building Rmd vignettes with knitr or rmarkdown.  
  - `r-data.table-dev`: extends `r-pkg` with data.table suggested dependencies, but no data.table itself.  
  - `r-data.table`: upgrades `r-base-dev` to Rserve service with data.table.  
  - `r-data.table-pg`: extends `r-data.table` service with native postgres drivers and RpostgreSQL, logR and pg R packages.  
