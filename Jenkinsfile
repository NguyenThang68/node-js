pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/NguyenThang68/node-js.git'
            }
        }
        stage('Buil stage'){
            steps {
                // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'ACR_LAB', url: 'https://myregistryaksnqt.azurecr.io') {
                    sh 'docker build -t thekop68/nodejs:v1 .'
                    sh 'docker tag thekop68/nodejs:v1 myregistryaksnqt.azurecr.io/nodejs:v1'
                    sh 'docker push myregistryaksnqt.azurecr.io/nodejs:v1'
                    //sh 'docker run -d -p 8081:8081 --name nodejs myregistryaksnqt.azurecr.io/nodejs:v1'
                }
            }
        }
        stage('Apply AKS'){
            steps {
                withkubeconfig(credentialsId: 'AKS_ID', serverUrl: 'https://jenkinaks-dns-4139fff3.hcp.eastus.azmk8s.io:443') {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}