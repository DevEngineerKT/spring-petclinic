pipeline {
    agent{
        docker {
            image 'maven:3.8.5-openjdk-11-slim'
            args '--add-host host.docker.internal:172.17.0.1 --network host'
        }

    }

    stages {
        stage('maven version') {
            steps{
                sh '''
                    mvn -version
                '''

            }

        }
        stage('sonarqube healthcheck') {
            steps{
                sh '''
                    curl --location --request GET 'http://host.docker.internal:9000/api/system/health' --header 'Authorization: Basic YWRtaW46RGVtb1BAc3N3b3JkMTIz'
                '''

            }

        }
        stage('Pull Source Code') {
            steps{
                sh '''
                    mvn compile
                '''

            }

        }
    }

}
