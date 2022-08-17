pipeline {
    agent any
    // TODO: add trigger for pollSCM
    environment {
        access_key = credentials('aws-cli-access-token')
        secret_key = credentials('aws-cli-secret-key')
    }
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
                    # TODO: figure out how to run docker commands in a docker container
                    # docker run --rm -it -v ~/.aws:/ubuntu/.aws amazon/aws-cli --version
                    
                    # Set env variables to configure aws-cli
                    export AWS_ACCESS_KEY_ID="${env.access_key}"
                    export AWS_SECRET_ACCESS_KEY="${env.secret_key}"
                    export AWS_DEFAULT_REGION=us-east-1
                    
                    aws --version
                    # aws s3api list-buckets --query "Buckets[].Name"
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