FROM docker.io/rocker/drd

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

# install qpdf for "--as-cran" R check
RUN apt-get update -qq \
  && apt-get install -y --no-install-recommends qpdf

# install pandoc required for building markdown vignettes
RUN PANDOC_VERSION='1.13.1' \
  && PANDOC_DIR="${HOME}/opt/pandoc" \
  && PANDOC_URL="https://s3.amazonaws.com/rstudio-buildtools/pandoc-${PANDOC_VERSION}.zip" \
  && mkdir -p "${PANDOC_DIR}" \
  && wget -O /tmp/pandoc-${PANDOC_VERSION}.zip ${PANDOC_URL} \
  && unzip -j /tmp/pandoc-${PANDOC_VERSION}.zip "pandoc-${PANDOC_VERSION}/linux/debian/x86_64/pandoc" -d "${PANDOC_DIR}" \
  && chmod +x "${PANDOC_DIR}/pandoc" \
  && ln -s "${PANDOC_DIR}/pandoc" /usr/local/bin \
  && unzip -j /tmp/pandoc-${PANDOC_VERSION}.zip "pandoc-${PANDOC_VERSION}/linux/debian/x86_64/pandoc-citeproc" -d "${PANDOC_DIR}" \
  && chmod +x "${PANDOC_DIR}/pandoc-citeproc" \
  && ln -s "${PANDOC_DIR}/pandoc-citeproc" /usr/local/bin

# install R packages
RUN RDscript -e 'install.packages(c("knitr","rmarkdown"))'

# install drat@artifacts with `insertArtifacts` function
RUN RDscript -e 'install.packages("drat", repos = "https://jangorecki.gitlab.io/drat")'

# R check envs
ENV _R_CHECK_CRAN_INCOMING_=FALSE
ENV _R_CHECK_FORCE_SUGGESTS_=TRUE

# start R-devel
CMD ["RD"]
