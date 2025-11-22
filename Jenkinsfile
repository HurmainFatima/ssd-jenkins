pipeline {
    agent any

    // Parameters for conditional execution
    parameters {
        booleanParam(
            name: 'executeTests',
            defaultValue: true,
            description: 'Check to run the Test stage'
        )
    }

    // Environment variables
    environment {
        VERSION = '1.0.0'
    }

    // Build tools
    tools {
        maven 'Maven' // Name must match your Jenkins Maven installation
        // Optional: jdk 'JDK 21' if configured in Jenkins
    }

    stages {

        stage('Build') {
            steps {
                echo "Building version ${VERSION}..."
                
                // Always print Maven version
                bat 'mvn -version'

                // Only run mvn clean install if pom.xml exists
                script {
                    if (fileExists('pom.xml')) {
                        bat 'mvn clean install'
                    } else {
                        echo 'No pom.xml found, skipping Maven build'
                    }
                }
            }
        }

        stage('Test') {
            when {
                expression { params.executeTests == true }
            }
            steps {
                echo "Running tests for version ${VERSION}..."
                
                script {
                    if (fileExists('pom.xml')) {
                        bat 'mvn test'
                    } else {
                        echo 'No pom.xml found, skipping tests'
                    }
                }
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
        success {
            echo 'Build Succeeded'
        }
        failure {
            echo 'Build Failed'
        }
    }
}
