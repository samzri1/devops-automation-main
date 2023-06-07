pipeline {
    agent any
    tools{
        maven 'mvn'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/samzri1/devops-automation-main']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t samzri/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u samzri -p dckr_pat_kRC0j5zg0C3mJhxQCeigH2xg0BA'}
                   sh 'docker push samzri/devops-integration'
                }
            }
        }
       stage('Deploy to vm'){
            steps{
                script{ 
                    sh ' ssh  sam@20.231.209.56'
                sh 'sshpass -p H1T8POVN21D4EE7Y$ ssh  sam@20.231.209.56 && docker pull samzri/devops-integration && docker run samzri/devops-integration'
              }
           }}
    }
}
