## Project Tit
## Chat-Interface Java Application Deployed on Docker-swarm cluster and placing Nginx as laodbalancer
## --------------------------------------------------------------------------
## Image
![project-7](https://user-images.githubusercontent.com/111736742/219126197-9d8d9c4d-0d54-4870-9523-6dc9caec9a52.jpg).
## ------------------------------------------------------------------------
## Requirements
- Jenkins
- SonarQube
- Nexus
- Docker-Hub,Dockerfile
- Docker-swarm Cluster(1M-2N)
- Nginx
## Docke-swarm cluster
![dockerswarmnodels](https://user-images.githubusercontent.com/111736742/219244606-456dc781-aed3-4127-a6ad-b1bac717d90b.png)

#sh "docker service create --name chat -p 8081:8080 --replicas 4 chaitu1812/chat-interface:latest"

#sh "docker service update --image chaitu1812/chat-interface:{params.Buildnumber} chat"

#sh "docker service rollback chat"

```bash
   Docker-Swarm Cluster
   ________________________________________
  docker-manager --> 13.232.126.234(public-ip)
  node-1--> 65.1.147.187(public-ip)
  node-2--> 65.2.161.155(public-ip)
  __________________________________________
  nginx-server-->3.110.204.147(public-ip)
```
## Jenkins-Dashboard
#with docker-swarm Cluster.
![jenkins-Dashboard](https://user-images.githubusercontent.com/111736742/219238533-039045cc-23ab-4a27-8eff-b57572888f5b.png)
## output
#SonarQube-Server
![dockerswarmsonar](https://user-images.githubusercontent.com/111736742/219246678-b6529976-0e61-4349-bb33-d79e60d86b6c.png)
#Nexus-server
![dockerswarmnexus](https://user-images.githubusercontent.com/111736742/219246784-294c1c40-19a7-49cc-808c-824628a7182e.png)

## -------------------------------------------------------------------------------------------
## Jenkins-Dashboard
#with docker-swarm clusterupdate.
![dockerswarmbuild](https://user-images.githubusercontent.com/111736742/219239443-18eb0beb-2f9b-4a61-b017-8ad68224f16d.png)
## output
![dockerswarmupdate](https://user-images.githubusercontent.com/111736742/219239640-72581af2-17b1-43c4-bb48-e59adccf9d16.png)

## ----------------------------------------------------------------------------------------------------
## Jenkins-Dashboard
#with docker-swarm Cluster rollback.

## ---------------------------------------------------------------------------------------------------
## Install nginx
To changes run the following command
```bash
  amazon-linux-extras install nginx1
  cd /etc/
  chmod 777 -R nginx
```
## Demo  
```bash
  vi nginx.conf
  -------------------------------------
events {}
http {
upstream chaitu{
server  Ip-address;                      
server  Ip-address;              
server  Ip-address;              
}

server {
        listen 9000; ---- you can change port number
      location / {
      proxy_pass http://chaitu;
      }
  }

}
 }
 ```
## finally with Nginx-server
![docker-swarmnginxserver](https://user-images.githubusercontent.com/111736742/219241507-db6fd744-9e72-40f8-a5e9-f83fb8d9deeb.png)
## Output
![Screenshot_20230216_064618](https://user-images.githubusercontent.com/111736742/219243941-2e5a162a-9215-41a8-b649-af789e2680b0.png)








