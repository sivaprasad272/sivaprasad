pipeline {
    agent any

    stages {
        stage('Example Stage') {
            steps {
                // Load global credentials of type "Secret Text" with ID 'aws-access-key'
                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY')
                    string(credentialsId: 'aws-access-key' ,variable: 'AWS_SECRET_KEY')
                ]) {
                    // Use the loaded credential in a step
                    sh "echo \$AWS_ACCESS_KEY"
                }
            }
        }
    }
}
