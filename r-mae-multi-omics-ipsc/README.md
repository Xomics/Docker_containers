# Docker container for using the MultiAssayExperiment object and running multi-omics analyses in R 


## Pull Docker image
```{bash}
# Dockerfile VERSION = v0.1
docker pull casperdevisser/r-mae-multi-omics-ipsc:$VERSION #latest
```

## Build Docker image s

```{bash}
docker build --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') -t casperdevisser/r-mae-multi-omics-ipsc:$VERSION . 
```