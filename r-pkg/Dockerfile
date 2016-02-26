FROM quay.io/jangorecki/r-base-dev

MAINTAINER Jan Gorecki j.gorecki@wit.edu.pl

# install qpdf for "--as-cran" R check
RUN add-apt-repository -y "ppa:marutter/rrutter" \
  && apt-get update -qq \
  && apt-get install -y --no-install-recommends qpdf

# install pandoc required for building markdown vignettes
RUN PANDOC_VERSION='1.13.1' \
  && PANDOC_DIR="${HOME}/opt/pandoc" \
  && PANDOC_URL="https://s3.amazonaws.com/rstudio-buildtools/pandoc-${PANDOC_VERSION}.zip" \
  && mkdir -p "${PANDOC_DIR}" \
  && curl -o /tmp/pandoc-${PANDOC_VERSION}.zip ${PANDOC_URL} \
  && unzip -j /tmp/pandoc-${PANDOC_VERSION}.zip "pandoc-${PANDOC_VERSION}/linux/debian/x86_64/pandoc" -d "${PANDOC_DIR}" \
  && chmod +x "${PANDOC_DIR}/pandoc" \
  && ln -s "${PANDOC_DIR}/pandoc" /usr/local/bin \
  && unzip -j /tmp/pandoc-${PANDOC_VERSION}.zip "pandoc-${PANDOC_VERSION}/linux/debian/x86_64/pandoc-citeproc" -d "${PANDOC_DIR}" \
  && chmod +x "${PANDOC_DIR}/pandoc-citeproc" \
  && ln -s "${PANDOC_DIR}/pandoc-citeproc" /usr/local/bin

# setup R repos
RUN echo 'options(repos = c(CRAN = "https://cran.rstudio.com"))' >> /etc/R/Rprofile.site

# install R packages
RUN Rscript -e 'install.packages(c("knitr","rmarkdown"))'

# explicitly override for `insertArtifacts` feature
RUN Rscript -e 'install.packages("drat", repos = "https://jangorecki.gitlab.io/drat")'

# R check envs
ENV _R_CHECK_CRAN_INCOMING_=false
ENV _R_CHECK_FORCE_SUGGESTS_=true

# start R
CMD ["R"]
