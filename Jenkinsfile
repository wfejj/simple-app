pipeline {
    agent any
    tools {
        maven 'maven3'
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
                    [
                        artifactId: 'simple-app',
                        classifier: '',
                        file: 'target/simple-app-1.0.0.war',
                        type: 'war'
                    ]
                ],
                    credentialsId: 'NEXUS3',
                    groupId: 'in.javahome',
                    nexusUrl: 'http://localhost:8081/',
                    nexusVersion: 'NEXUS3', protocol: 'http',
                    repository: 'http://localhost:8081/repository/simpleapp-release/',
                    version: '1.0.0' 
            }
        }
    }
}
