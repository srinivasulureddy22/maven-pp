pipeline {
    agent any
     tools {
        maven 'maven' 
    }
    stages {
        stage('clone') {
            steps{
               git credentialsId: 'gtihublogin', url: 'https://github.com/srinivasulureddy22/maven-pp.git'
            }
        }
        stage('maven version') {
            steps{
               sh 'mvn --version'
            }
        }
        stage('maven') {
            steps{
               sh 'mvn clean install'
            }
        }
        stage("build & SonarQube Scanner") {
            steps {
              withSonarQubeEnv('sonarqube') {
                sh 'mvn clean package sonar:sonar'
              }
            }
        } 
        stage('Docker_login') {
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                        sh "docker build -t cicd ."
                }
              }
             }
           }
        stage('Docker-push') {
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                        sh "docker tag cicd rishitha/end-to-end:BUILED_ID"
                        sh "docker push rishitha/end-to-end:BUILED_ID"
                }
               }
              }
            }
            
 }
}
