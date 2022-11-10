pipeline {
    agent none
    stages {
        stage('Sonarqube') {
            agent any
            steps {
                def scannerHome = tool name: 'sonar_scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation';
                withSonarQubeEnv('SonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Build') { 
            agent {
                docker {
                    image 'maven:3.8.1-adoptopenjdk-11'
                    args '-v /root/.m2:/root/.m2'
                }
            }
            steps {
                sh 'mvn clean install -Dcheckstyle.skip' 
            }
        }
    }
}