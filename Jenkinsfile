pipeline {
    agent any
    // TODO: add trigger for pollSCM
    stages {
        stage('Clone number-guesser repo') {
            steps {
                echo 'Cloning number-guesser repo to local workspace'
                git branch: 'master',
                    credentialsId: 'git-access-token',
                    url: 'https://github.com/jenkinsci/jenkins.git'

            }
        }
        stage('Upload app files to s3') {
            steps {
                echo 'Uploading files to s3'
                sh '''
                    // TODO: figure out how to run docker commands in a docker container
                    // docker run --rm -it -v ~/.aws:/ubuntu/.aws amazon/aws-cli --version
                    aws --version
                    aws s3api list-buckets --query "Buckets[].Name"
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