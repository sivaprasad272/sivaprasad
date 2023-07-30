pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    sh "git status"
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
                        string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_KEY')
                    ]) {
                        sh "aws --version"
                        sh "aws configure list"
                        sh "aws configure --profile"
                        sh "aws configure set aws_access_key_id \$AWS_ACCESS_KEY"
                        sh "aws configure set aws_secret_access_key \$AWS_SECRET_KEY"
                        sh "aws configure set default.region ap-south-1 // Replace with your desired default region"
                        sh "aws configure set default.output json // Replace with your desired output format"
                        sh "aws s3 cp \$WORKSPACE/index.html s3://kulfibucket/"
                    }
                }
            }
        }
    }
}
