pipeline {
  agent {
    docker {
      image 'maven:3.9.5-openjdk-21'
      args '-v /tmp:/tmp'
    }

  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Test') {
      post {
        always {
          junit '**/target/surefire-reports/*.xml'
        }

      }
      steps {
        sh 'mvn test'
      }
    }

    stage('Verify') {
      steps {
        sh 'mvn verify'
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