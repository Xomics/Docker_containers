# Muon Docker container
Docker container for working with Muon and MuData

## How to run the Docker Container
```
docker run -it -v $(volume):/container/ -p 8888:8888 casperdevisser/muon:v0.2 #check correct version
```

- **$(volume)** is the absolute path to directory where you store input data. 
Mount current directory, Windows Command Line: 'docker run -it -v %cd%:/container/ ...', PowerShell: 'docker run -it -v ${PWD}:/container/ ...', Linux: 'docker run -it -v $(pwd):/container/ ...'

- Open `localhost:8888` in a browser (outside of the docker). 

- If running the container inside the Windows DRE, use the ip-adress that is returned by the command `docker-machine ip`. For example: `xxx.xxx.xx.xx:8888`. 

- If token is required for login, copy paste the token that can be found in one of the URLs that is given as output after the docker run command. 
