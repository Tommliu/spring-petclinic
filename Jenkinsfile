pipeline {
    agent none
    stages {
        stage('Build') { 
            agent {
            docker {
                    image 'maven:3.8.1-adoptopenjdk-11'
                    args '-u Tom'
                    args '-v /root/.m2:/root/.m2'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh 'mvn clean install -Dcheckstyle.skip' 
            }
        }
        stage('App Docker Build') {
            agent any
            steps {
                sh 'docker ps'
                sh 'docker build -t petclinic:latest app/' 
            }
        }
    }
}