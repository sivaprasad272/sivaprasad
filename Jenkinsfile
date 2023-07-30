pipeline {
    agent any
    environment{
        export AWS-ACCESS-KEY='aws-access-key'
        export AWS-SECRET-KEY='aws-secret-key'
    }
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
                script{
                    sh "echo $AWS-ACCESS-KEY"
                    sh "echo $AWS-SECRET-KEY"
                    }
                }
           }
     }
}
