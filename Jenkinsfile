pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                script{
                sh "git status"
                sh "ls -la"
                sh "rm -f s3demo"
                sh "git clone https://github.com/sivaprasad272/s3demo.git"
                sh "export AWS_ACCESS_KEY='$aws-access-key'"
                sh "export AWS_SECRET_KEY='$aws-secret-key'"
                }
            }
        }
    }
}
