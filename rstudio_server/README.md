# Docker container for using the Rstudio server


## Build Docker image 
```{bash}
# Dockerfile VERSION = v0.1
docker build --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') -t casperdevisser/rstudio_server:$VERSION . 

```