pipeline {
    agent any

    environment {
        VERSION = '1.0.0'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building project version ${VERSION}..."
            }
        }

        stage('Test') {
            when {
                expression { params.executeTests == true }
            }
            steps {
                echo "Running tests for version ${VERSION}..."
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying version ${VERSION}..."
            }
        }
    }

    post {
        always {
            echo "Pipeline Completed for version ${VERSION}"
        }
    }
}
