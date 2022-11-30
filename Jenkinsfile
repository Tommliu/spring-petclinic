pipeline {
    agent none
    stages {
        // stage('Sonarqube') {
        //     agent any
        //     environment {
        //         scannerHome = tool 'SonarQubeScanner'
        //     }
        //     steps {
        //         withSonarQubeEnv('SonarQube') {
        //             sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=develop -Dsonar.java.binaries=. -Dsonar.sources=./src"
        //         }
        //     }
        // }
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

        stage('Transfer') {
            agent any
            steps {
                sh 'scp /var/jenkins_home/workspace/spring-petclinic-docker/?/.m2/repository/org/springframework/samples/spring-petclinic/2.7.3/spring-petclinic-2.7.3.jar root@192.168.1.19:/spring-petclinic-2.7.3.jar'
            }
        }

        stage('Deploy petclinic') {
            agent any
            steps {
                ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible2', inventory: 'inventory.ini', playbook: 'playbook.yml'
            }
        }
    }
}