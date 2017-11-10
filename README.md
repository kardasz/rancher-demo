## Rancher Demo

* Rancher Quick Start Guide http://rancher.com/docs/rancher/latest/en/quick-start-guide/
* Docker install http://rancher.com/docs/rancher/v1.6/en/hosts/#supported-docker-versions
* Rancher install http://rancher.com/docs/rancher/v1.6/en/installing-rancher/installing-server/#single-container

### 1. Rancher setup

* `vagrant ssh rancher` go to vagrant vm where we place rancher server
* `sudo docker run -d --restart=unless-stopped -p 8080:8080 rancher/server` start rancher server
* http://172.12.12.10:8080 open rancher GUI 

### 2. Add Agents

* http://172.12.12.10:8080 click Add Host
* `vagrant ssh vm1` go to vagrant vm first managed node
* Run rancher custom agent 
* `vagrant ssh vm2` go to vagrant vm second managed node
* Run rancher custom agent
