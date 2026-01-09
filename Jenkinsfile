pipeline {
    agent any

    tools {
        maven 'Maven3'   // Make sure Maven is configured in Jenkins
        jdk 'JDK11'      // Or the JDK installed in Jenkins
    }

    environment {
        BUILD_DIR = "target"
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Cloning repository..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building the Maven project..."
                sh "mvn clean compile"
            }
        }

        stage('Test') {
            steps {
                echo "Running unit tests..."
                sh "mvn test"
            }
        }

        stage('Package') {
            steps {
                echo "Packaging the application..."
                sh "mvn package"
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
        always {
            cleanWs()
        }
    }
}
