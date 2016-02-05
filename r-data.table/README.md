
# data.table as a service/node

Based on dockerfile for minimal setup of Ubuntu, R and the packages Rserve and data.table, [jangorecki/r-base-dev](https://hub.docker.com/r/jangorecki/r-base-dev/) which is:

```
ubuntu + git + ssl + curl + r-base-dev
```

Additionally, providing [Rserve](https://github.com/s-u/Rserve) and [data.table](https://github.com/Rdatatable/data.table) packages.  
Rserve instance is configured and started. Encoding is set to utf8, unlike Rserve default.  

# How to start

Start a node in shell.

```sh
docker run -d -p 33311:6311 --name=rnode11 jangorecki/r-data.table
```

# How to connect

Connect from R session.

```r
library(data.table)
library(RSclient)
conn = RS.connect(port = 33311)
dt = RS.eval(conn, as.data.table(iris))
str(dt)
RS.close(conn)
```

# How to make cluster

Run 3 more nodes from shell.

```sh
docker run -d -p 33312:6311 --name=rnode12 jangorecki/r-data.table
docker run -d -p 33313:6311 --name=rnode13 jangorecki/r-data.table
docker run -d -p 33314:6311 --name=rnode14 jangorecki/r-data.table
```

Use base R `lapply` function to manage nodes as list.

```r
port = 33311:33314
rscl = lapply(port, function(port) RS.connect(port=port))
lapply(rscl, RS.eval, {x <- as.data.table(iris); TRUE})
lapply(rscl, RS.eval, x[, lapply(.SD, mean), Species])
lapply(rscl, RS.close)
```

Stop docker Rserve services.  

```sh
docker stop rnode11 rnode12 rnode13 rnode14
```

# Using big.data.table class

Follow readme on [big.data.table](https://gitlab.com/jangorecki/big.data.table) package, it provides `big.data.table` class which is an extended wrapper on above `lapply`, running queries in parallel, row binding results and much more.  
