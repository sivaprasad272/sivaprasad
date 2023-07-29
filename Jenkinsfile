pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                sh "git status"
                sh "ls -la"
                sh "git clone https://github.com/sivaprasad272/sivaprasad.git"
            }
        }
        stage('Check AWS Profile') {
            steps {
                // Load AWS access credentials from Jenkins credentials
                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
                    // Configure AWS CLI using the credentials from Jenkins credentials
                    sh """
                        aws configure set aws_access_key_id \${AWS_ACCESS_KEY_ID}
                        aws configure set aws_secret_access_key \${AWS_SECRET_ACCESS_KEY}
                        aws configure set default.region us-west-2 // Replace with your desired default region
                        aws configure set default.output json // Replace with your desired output format
                    """
                    // Use the AWS CLI to copy the index.html file to S3
                    sh "aws s3 cp $WORKSPACE/index.html s3://kulfibucket/"
                }
            }
        }
    }
}
