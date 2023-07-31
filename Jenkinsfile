pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    sh "rm -rf s3demo"
                    sh "ls -la"
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
                    input(message: 'Enter AWS region (e.g., ap-south-1): ', parameters: [
                        string(defaultValue: 'ap-south-1', description: 'AWS region', name: 'AWS_REGION')
                    ])
                    input(message: 'Enter AWS output format (e.g., json): ', parameters: [
                        string(defaultValue: 'json', description: 'Output format', name: 'AWS_OUTPUT')
                    ]) 
                        sh "aws --version"
                        sh "aws configure list"
                       
                        sh "aws configure set aws_access_key_id \$AWS_ACCESS_KEY"
                        sh "aws configure set aws_secret_access_key \$AWS_SECRET_KEY"
                        sh "aws configure set default.region \${AWS_REGION}"
                        sh "aws configure set default.output \$AWS_OUTPUT" // Corrected variable name here
                        sh "aws s3 cp \$WORKSPACE/index.html s3://kulfibucket/" 
                        }
                    }
                }
            }
        }
    }
}
