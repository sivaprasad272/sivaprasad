pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                sh "git status"
                sh "ls -la"
                sh "git clone https://github.com/sivaprasad272/s3demo.git"
                sh "export AWS_ACCESS_KEY='$aws-access-key'"
                sh "export AWS_SECRET_KEY='$aws-secret-key'"
            }
        }
        stage('check aws profile') {
            steps {
                script {
                   // sh "aws --version"
                    sh "aws configure list"
                    sh "aws configure --profile"
                    sh "aws configure set aws_access_key_id \$AWS_ACCESS_KEY"
                    sh "aws configure set aws_secret_access_key \$AWS_SECRET_KEY"
                    sh "aws configure set default.region us-west-2 // Replace with your desired default region"
                    sh "aws configure set default.output json // Replace with your desired output format"
                    sh "aws s3 cp \$WORKSPACE/index.html s3://kulfibucket/"  //
                }
            }
        }
    }
}
