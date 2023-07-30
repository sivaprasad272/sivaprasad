pipeline {
    agent any

    stages {
        stage('Example Stage') {
            steps {
                // Load global credentials of type "Secret Text" with ID 'aws-access-key'
                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY')
                ]) {
                    // Use the loaded AWS_ACCESS_KEY in a step
                    sh "echo \$AWS_ACCESS_KEY"
                }
                
                // Load global credentials of type "Secret Text" with ID 'aws-secret-key'
                withCredentials([
                    string(credentialsId: 'aws-secret_key', variable: 'AWS_SECRET_KEY')
                ]) {
                    // Use the loaded AWS_SECRET_KEY in a step
                    sh "echo \$AWS_SECRET_KEY"
                }
            }
        }
    }
}
