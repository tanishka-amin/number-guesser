pipeline {
    agent any
    triggers { cron('H 20 * * *') }
    environment {
        access_key = credentials('aws-cli-access-token')
        secret_key = credentials('aws-cli-secret-key')
    }
    stages {
        stage('Clone number-guesser repo') {
            steps {
                echo 'Cloning number-guesser repo to local workspace'
                git branch: 'main',
                    credentialsId: 'git-access-token',
                    url: 'https://github.com/tanishka-amin/number-guesser.git'
            }
        }
        stage('Upload app files to s3') {
            steps {
                echo 'Uploading files to s3'
                sh '''
                    # TODO: figure out how to run docker commands in a docker container
                    # docker run --rm -it -v ~/.aws:/ubuntu/.aws amazon/aws-cli --version
                    
                    # Set env variables to configure aws-cli
                    export AWS_ACCESS_KEY_ID="${access_key}"
                    export AWS_SECRET_ACCESS_KEY="${secret_key}"
                    export AWS_DEFAULT_REGION=us-east-1
                    
                    aws --version
                    
                    aws s3api list-buckets --query "Buckets[].Name"
                    
                    # aws s3 sync . s3://simplenumberguesser.com --delete --exclude "Jenkinsfile" --exclude ".git/*" --dryrun
                    aws s3 sync . s3://simplenumberguesser.com --delete --exclude "Jenkinsfile" --exclude ".git/*"
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