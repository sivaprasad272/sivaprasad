pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                script{
                sh "git status"
                sh "ls -la"
                sh "rm -rf sivaprasad"
                sh "git clone https://github.com/sivaprasad272/sivaprasad.git"
                sh "export AWS_ACCESS_KEY=\"$aws-access-key\""
                sh "export AWS_SECRET_KEY=\"$aws-secret-key\""

                }
            }
        }
    }
}
