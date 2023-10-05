pipeline {
    triggers {
  pollSCM('* * * * *')
    }
   agent any
    tools {
  maven 'M2_HOME'
  }

   environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "45.79.56.117:8081"
        NEXUS_REPOSITORY = "nexus-pipeline"
        NEXUS_CREDENTIAL_ID = "nexus-user-credentials"

        
        imageName = "fastfood"
        registryCredentials = "nexus-user-credentials"
        registry = "45.79.56.117:8085/repository/nexus-registry/"
        dockerImage = ''
    }

    stages {
        stage("Maven Build Back-End") {
            steps {
                echo 'Build Back-End Project...'
                dir('./fastfood_backend/'){
                    script {
                    sh "mvn package -DskipTests=true -Dspring.profiles.active=test"
                    }
                }
            }
        }

         // Building Docker images
        stage("Build Docker Image"){
            steps{
                echo 'Build Docker Image'
                dir('./fastfood_BackEnd/'){
                    script{
                        dockerImage = docker.build imageName
                    }
                }
            }
        }
   
        // Push Docker images to Nexus Registry
        stage("Uploading to Nexus Registry"){
            steps{
                echo 'Uploading Docker image to Nexus ...'
                dir('./fastfood_BackEnd/'){
                    script{
                        docker.withRegistry( 'http://'+registry, registryCredentials ) {
                        dockerImage.push('latest')
                        }
                    }
                }
            }
        }      
    }
} 
      