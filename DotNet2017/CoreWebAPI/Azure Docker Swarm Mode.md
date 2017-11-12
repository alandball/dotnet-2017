Use [ACS Engine swarm mode](https://azure.microsoft.com/en-us/resources/templates/101-acsengine-swarmmode/) as the default ACS uses standalone Swarm cluster which is quite old.

Deploy Azure Container Service in Docker Swarm mode with follwoing options

## Azure container service setting
Name : coredemo
resource Group : swarmresourcegroup
Location : Southeast Asia
Master prefix : swarmmaster
Master user credential : swarmdmin
Agent prefix : swarmagent

open SSH tunnel to Swarm endpoint in SE Asia
```bash

ssh -fNL 2375:localhost:2375 -p 2200 swarmadmin@swarmmaster.southeastasia.cloudapp.azure.com
```

Set DOCKER_HOST environment variable

```bash
export DOCKER_HOST=:2375
```
### ListDocker swarm nodes
```bash
docker node ls

docker node ps

```

### Deploy stack to Swarm nodes with stackname `webapp`
```bash
docker stack deploy -c docker-compose.azure.yml webapp
```

### List stacks
```bash
docker stack ls
```

### List tasks in `webapp` stack
```bash
docker stack ps webapp
```

### List all services
```bash
docker service ls
```

### List all tasks related to `coremvc`
```bash
docker service ps webapp_coremvc
```

### List all tasks related to `corewebapi`
```bash
docker service ps webapp_corewebapi
```

## Scale services
### Scale `Coremvc` service to 2 replicas
```bash
docker service scale webapp_coremvc=2
```

### Scale `corewebapi` service to 3 replicas
```bash
docker service scale webapp_corewebapi=3
```

## Pull down the whole stack
```bash
docker stack rm webapp
```