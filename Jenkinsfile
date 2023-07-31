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
                        // Prompt user for AWS region and output format
                        input(message: 'Enter AWS region (e.g., ap-south-1): ', parameters: [
                            string(defaultValue: 'ap-south-1', description: 'AWS region', name: 'AWS_REGION')
                        ])
                        input(message: 'Enter AWS output format (e.g., json): ', parameters: [
                            string(defaultValue: 'json', description: 'Output format', name: 'AWS_OUTPUT')
                        ]) 
                        
                        // Display AWS CLI version and configuration for verification
                        sh "aws --version"
                        sh "aws configure list"

                        // Configure AWS CLI using provided credentials and inputs
                        sh "aws configure set aws_access_key_id \$AWS_ACCESS_KEY"
                        sh "aws configure set aws_secret_access_key \$AWS_SECRET_KEY"
                        sh "aws configure set region \${AWS_REGION}"
                        sh "aws configure set output \${AWS_OUTPUT}"
                        
                        // Copy 'index.html' to S3 bucket
                        sh "aws s3 cp \$WORKSPACE/s3demo/index.html s3://kulfibucket/"
                    }
                }
            }
        }
    }
}
