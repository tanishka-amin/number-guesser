pipeline {
    agent any
    // TODO: add trigger for pollSCM
    stages {
        stage('Clone number-guesser repo') {
            steps {
                echo 'Cloning number-guesser repo to local workspace'
                git branch: 'master',
                    credentialsID: 'git-access-token'
                    url: 'https://github.com/jenkinsci/jenkins.git'

            }
        }
        stage('Upload app files to s3') {
            steps {
                echo 'Uploading files to s3'
                sh '''
                    docker run --rm -it -v ~/.aws:/ubuntu/.aws amazon/aws-cli --version
                '''
            }
        }
        stage('Test URL') {
            steps {
                echo 'Testing url'
            }
        }
    }
}