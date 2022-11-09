pipeline {
    agent {
        docker {
            image 'maven:3.8.1-adoptopenjdk-11'
            args '-u Tom'
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn clean install -Dcheckstyle.skip' 
            }
        }
        stage('Run') {
            steps {
                sh 'java -jar target/*.jar'
            }
        }
    }
}