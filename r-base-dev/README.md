Dockerfile for minimal setup of Ubuntu and R
```
ubuntu + git + ssl + curl + vim + r-base-dev
```
None of R packages are installed.

Following R options are set in `/etc/R/Rprofile.site`
```
options(
  repos = c(CRAN = "https://cloud.r-project.org"),
  download.file.method = "libcurl"
)
```
