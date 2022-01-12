pipeline {
    agent any
    
    tools {
        maven 'Maven'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    
    
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                 nexusArtifactUploader artifacts: [
                [artifactId: 'simple-app', classifier: '', 
                 file: 'target/simple-app-3.0.0.war', type: 'war']], 
                 credentialsId: '0fc796ec-1b06-40c0-850a-a5e2914ea0b0',
                 groupId: 'in.javahome', nexusUrl: '172.19.9.28:8081',
                 nexusVersion: 'nexus3', protocol: 'http', 
                 repository: 'simpleapp-release', version: '3.0.0'
            }
        }
         
    }
}
