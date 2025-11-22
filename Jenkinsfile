pipeline {
    agent any

    tools {
        maven 'Maven' // Name of the Maven installation configured in Jenkins
        jdk 'JDK 21'  // Optional: specify JDK if needed
    }

    environment {
        VERSION = '1.0.0'
    }

    stages {
        stage('Build') {
            steps {
                // On Windows, use bat instead of sh
                bat 'mvn -version'
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            when {
                expression { params.executeTests == true }
            }
            steps {
                bat 'mvn test'
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
