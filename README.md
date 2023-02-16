## Project Title
## Chat-Interface Java Application Deployed on Docker-swarm cluster and placing Nginx as laodbalancer
## ---------------------------------------------------------------------------------------------------
## Image
![project-7](https://user-images.githubusercontent.com/111736742/219126197-9d8d9c4d-0d54-4870-9523-6dc9caec9a52.jpg).
## -------------------------------------------------------------------------------------------------
## Requirements
- Jenkins
- SonarQube
- Nexus
- Docker-Hub,Dockerfile
- Docker-swarm Cluster(1-2)
- Nginx-server
## Docke-swarm cluster

sh "docker service create --name chatin -p 8081:8080 --replicas 4 chaitu1812/chat-interface:latest"

```bash
   sonar -->
  docker-manager --> 13.232.126.234(public-ip)
  node-1--> 65.1.147.187(public-ip)
  node-2--> 65.2.161.155(public-ip)
  nginx-server-->3.110.204.147(public-ip)
```
