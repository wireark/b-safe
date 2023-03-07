pipeline { 
agent any
    stages {
        stage ('Pull Docker Image from the Docker Hub') {
            steps{
                sh '''docker pull wireark/gs-spring-boot-docker:latest'''
                echo 'Getting the docker image'
            }
        }
        stage ('Run Docker image') {
            steps{
                sh '''docker run -p 8080:8080 gs-spring-boot-docker -dt &'''
                echo 'Sleeping to start ...................'
                sh '''sleep 10'''
            }
        }
        stage ('Test Code') {
            steps {
                sh '''curl --head --silent --fail http://localhost:8080'''
                echo 'Test Results' 

            }
        }
        stage ('Remove Container Stack '){
            steps{
                echo 'docker rm $(docker stop $(docker ps -a -q --filter ancestor=gs-spring-boot-docker --format="{{.ID}}"))' 
            }
        }
    }
}

