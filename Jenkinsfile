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

         
    
        stage('Check Quality Gate') {
            steps {
                echo 'Checking quality gate...'
                dir('./fastfood_BackEnd/'){ 
                    script {
                    timeout(time: 20, unit: 'MINUTES') {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline stopped because of quality gate status: ${qg.status}"
                            } 
                        }
                    }
                }
            }
        }
    }
} 
      