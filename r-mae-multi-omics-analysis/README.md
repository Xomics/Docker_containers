# Docker container for using the MultiAssayExperiment object and running multi-omics analyses in R 


## Pull Docker image
```{bash}
docker pull casperdevisser/r-mae-multi-omics-analysis:v0.4 #latest
```

## Build Docker image 

```{bash}
# Dockerfile VERSION = v0.4
docker build --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') -t casperdevisser/r-mae-multi-omics-analysis:$VERSION . 
```