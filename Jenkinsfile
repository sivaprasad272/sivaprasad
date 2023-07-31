pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Remove existing 's3demo' directory and clone GitHub repository
                    sh "rm -rf s3demo"
                    sh "git clone https://github.com/sivaprasad272/s3demo.git"
                }
            }
        }
        stage('AWS Tasks') {
            steps {
                script {
                    // Load AWS access credentials from Jenkins credentials and set as environment variables
                    withCredentials([
                        string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY'),
                        string(credentialsId: 'aws-secret_key', variable: 'AWS_SECRET_KEY')
                    ]) {
                        // Display AWS CLI version and configuration for verification
                        sh "aws --version"
                        sh "aws configure list"

                        // Set AWS region and output format as environment variables
                        env.AWS_REGION = "${params.AWS_REGION}"
                        env.AWS_OUTPUT = "${params.AWS_OUTPUT}"

                        // Use environment variables for AWS CLI commands
                        sh "aws configure set aws_access_key_id \$AWS_ACCESS_KEY"
                        sh "aws configure set aws_secret_access_key \$AWS_SECRET_KEY"
                        sh "aws configure set default.region ap-south-1"
                        sh "aws configure set default.output table"
                        
                        // Copy 'index.html' to S3 bucket
                        sh "aws s3 cp \$WORKSPACE/s3demo/index.html s3://kulfibucket/"
                    }
                }
            }
        }
    }
}
