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
![dockerswarmlatest](https://user-images.githubusercontent.com/111736742/219238933-a8932899-70a2-49b1-90bf-728b0bd5c11e.png)
## -------------------------------------------------------------------------------------------
## Jenkins-Dashboard
#with docker-swarm clusterupdate.
![dockerswarmbuild](https://user-images.githubusercontent.com/111736742/219239443-18eb0beb-2f9b-4a61-b017-8ad68224f16d.png)
## output
![dockerswarmupdate](https://user-images.githubusercontent.com/111736742/219239640-72581af2-17b1-43c4-bb48-e59adccf9d16.png)
![dockerswarm](https://user-images.githubusercontent.com/111736742/219240080-235e7245-c76f-4ed1-b684-72221018e732.png)
## ----------------------------------------------------------------------------------------------------
## Jenkins-Dashboard
#with docker-swarm Cluster rollback.
![dockerswarmroolback](https://user-images.githubusercontent.com/111736742/219240566-ae8f81b8-df49-44c2-8771-14f09ed07cf2.png)
## output
![dockerswarmlatest](https://user-images.githubusercontent.com/111736742/219240827-ee83f484-c14f-4d00-9d3e-7074cd2935e3.png)
## ---------------------------------------------------------------------------------------------------
## finally with Nginx-server
![docker-swarmnginxserver](https://user-images.githubusercontent.com/111736742/219241507-db6fd744-9e72-40f8-a5e9-f83fb8d9deeb.png)
## Output
![Screenshot_20230216_064618](https://user-images.githubusercontent.com/111736742/219243941-2e5a162a-9215-41a8-b649-af789e2680b0.png)
![nginx-serverimage1](https://user-images.githubusercontent.com/111736742/219243647-fb2ed9dc-4f3f-4262-80b9-397fdff4f32a.png)







