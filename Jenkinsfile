pipeline {
    agent any
    environment {
        ACR_LOGINSERVER = credentials('ACR_LOGINSERVER')
    	ACR_ID = credentials('ACR_ID')
		ACR_PASSWORD = credentials('ACR_PASSWORD')
    }
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/NguyenThang68/node-js.git'
            }
        }
        stage('Buil stage'){
            steps {
                // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'ACR', url: 'https://azureregistryjenkins.azurecr.io') {
                    sh 'docker build -t thekop68/nodejs:v1 .'
                    sh 'docker tag thekop68/nodejs:v1 azureregistryjenkins.azurecr.io/nodejs:v2'
                    sh 'docker push azureregistryjenkins.azurecr.io/nodejs:v1'
                    sh 'docker run -d -p 8081:8081 --name nodejscacr azureregistryjenkins.azurecr.io/nodejs:v2'
                }
            }
        }
    }
}