pipeline {
    agent {
        docker {
            image 'maven:3.9.5-openjdk-21' // Use the official Maven Docker image
            args '-v /tmp:/tmp' // Optional: Mount a volume for caching or sharing files
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm // Check out the source code from SCM (e.g., Git)
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests' // Build the project without running tests
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test' // Run unit tests
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml' // Publish test results
                }
            }
        }
        stage('Verify') {
            steps {
                sh 'mvn verify' // Run integration tests and verify the build
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
