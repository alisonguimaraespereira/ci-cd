# DEVSECOPS ENVIRONMENT
Full stack tools for testing the local devsecops environment and other stuff.
- Prometheus
- Docker
- Grafana
- Jenkins


# How to
First of all, clone the ci-cd repo:
```
# git clone https://github.com/guimaraesasp/ci-cd.git
```

## Install Docker and create Swarm cluster
```
# curl -fsSL https://get.docker.com | sh
# docker swarm init
```

## Deploy Stack with Docker Swarm

Execute deploy to create the stack of devsecops:
```
# docker stack deploy -c docker-compose.yml devsecops

CCreating network devsecops_backend
Creating network devsecops_frontend
Creating service devsecops_grafana
Creating service devsecops_prometheus
Creating service devsecops_jenkins

```

Verify if services are ok:
```
# docker service ls

ID                  NAME                   MODE                REPLICAS            IMAGE                                PORTS
uw784ehhet8d        devsecops_grafana      replicated          1/1                 grafana/grafana:latest               *:3000->3000/tcp
o45jlu6w5ywu        devsecops_jenkins      replicated          1/1                 jenkins-master:latest                *:443->8443/tcp, *:8080->8080/tcp, *:50000->50000/tcp
m4tegpljd7x9        devsecops_prometheus   replicated          1/1                 linuxtips/prometheus_alpine:latest   *:9090->9090/tcp

```

## Access Services in Browser

To access Jenkins interface on browser:
```
http://YOUR_IP:8080
user: admin
passwd: devsecops
```

To access Prometheus interface on browser:
```
http://YOUR_IP:9090
```

To access Grafana interface on browser:
```
http://YOUR_IP:3000
user: admin
passwd: devsecops

To add plugs edit file ci-cd/grafana.config
GF_INSTALL_PLUGINS=plug1,plug2
```

