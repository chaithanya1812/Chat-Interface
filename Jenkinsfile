def loop = [
    mavenbuild: "mvn clean package",
    sonarQube: "mvn sonar:sonar",
    NexusArtifacts: "mvn deploy"
    ]
pipeline {
    agent { label 'jenkins-slave' }
    tools {
        maven 'MAVEN3.8.7'
    }
   parameters {
    string defaultValue: 'latest', description: 'for service update give the Build-ID', name: 'Buildnumber'
    choice choices: ['0', '1'], description: 'if you want to  go rollback select "1"  then otherwise select   "0"', name: 'rollback'
       }

    stages{
        stage('GitHub-webhook'){
            steps{
                script{
                    properties([pipelineTriggers([githubPush()])])
                }
            }
        }
        stage('Gitclone'){
            steps{
                git branch: 'FIRST', url: 'https://github.com/chaithanya1812/test6-Dockerswarm.git'
            }
        }
        stage('looping'){
            steps{
                script{
                    loop.each { entry ->
                    stage(entry.key){
                        sh "$entry.value"
                    }
                    
                    }
                }
            }
            
        }
        stage('dockerlogin and push'){
            steps {
            withCredentials([string(credentialsId: 'ddockerloginn', variable: 'dockerlogin')]) {
                sh 'docker login -u chaitu1812 --password $dockerlogin || true'    
            }
            sh 'docker build -t chaitu1812/chat-interface:latest .'
            sh 'docker build -t chaitu1812/chat-interface:$BUILD_ID .'
            sh 'docker push chaitu1812/chat-interface:latest'
            sh 'docker push  chaitu1812/chat-interface:$BUILD_ID'
            sh 'docker rmi chaitu1812/chat-interface:latest || true'
            sh 'docker rmi  chaitu1812/chat-interface:$BUILD_ID || true'
            
            }
        }
        stage('Docker-swarmcluster'){
             when {
                    expression { "${params.Buildnumber}" == "latest" &&  "${params.rollback}" == "0" }
                }
            
            steps{
                script{
                    def serviceremove = "docker service rm chat"
                    def service = "docker service create --name chat -p 8081:8080 --replicas 4 chaitu1812/chat-interface:latest"
                    sshagent(credentials: ['dockerswarm'], ignoreMissing: true) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.126.234 $serviceremove || true" 
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.126.234 $service"  
                    
                    }
                }
            }
        }
        stage('Docker-swarmupdate'){
            when {
                    expression { "${params.Buildnumber}" != "latest"  && "${params.rollback}" == "0" }
                 }
            steps{
                    sshagent(credentials: ['dockerswarm'], ignoreMissing: true) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.126.234 docker service update --image chaitu1812/chat-interface:${params.Buildnumber} chat"   
                    }
            }
        }
        stage('Docker-swarmRollback'){
            when {
                    expression { "${params.rollback}" == "1" }
                 }
            steps{
                script{
                    def servicerollback = "docker service rollback chat"
                    sshagent(credentials: ['dockerswarm'], ignoreMissing: true) {
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.126.234 $servicerollback"   
                    }
                }
            }
        }
           stage('Nginx-server'){
            steps{
                   sshagent(['nginx']) {
                    sh "scp -o StrictHostKeyChecking=no nginx.conf ec2-user@3.110.204.147:/etc/nginx/nginx.conf || true"
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@3.110.204.147 sudo systemctl restart nginx || true"
               }
            }
        }
            
    }
    
}
