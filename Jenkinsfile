pipeline {
    agent {
        docker {
            image 'maven:3.8.5-openjdk-11-slim'
        }
    }

    stages {
        stage('maven version') {
            steps {
                sh '''
                    mvn -version
                '''
            }
        }
        stage('sonarqube healthcheck') {
            steps {
                sh '''
                    curl --location --request GET 'http://tools-demo.cante-it-adventure.com:9000/api/system/health' \
                    --header 'Authorization: Basic YWRtaW46cEBzc3dvcmQxMjM0'
                '''
            }
        }
        stage('compile code') {
            steps {
                sh '''
                    mvn clean compile -Dcheckstyle.skip
                '''
            }
        }

        // stage('sonarQube analysis') {
        //     steps {
        //         withSonarQubeEnv('sonarqube-9.4') { // You can override the credential to be used
        //             sh '''
        //                 mvn clean verify sonar:sonar -Dcheckstyle.skip
        //             '''
        //         }
        //     }
        // }
    }
}
