pipeline {
    agent any

    parameters {
        booleanParam(
            name: 'executeTests',
            defaultValue: true,
            description: 'Check to run the Test stage'
        )
    }

    environment {
        VERSION = '1.0.0'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building version ${VERSION}..."
                bat 'mvn -version'
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
