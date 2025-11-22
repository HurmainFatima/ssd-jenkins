pipeline {
    agent any

    // -----------------------
    // Parameters (Step 12)
    // -----------------------
    parameters {
        booleanParam(
            name: 'executeTests',
            defaultValue: true,
            description: 'Check to run the Test stage'
        )
    }

    // -----------------------
    // Environment Variables (Step 10)
    // -----------------------
    environment {
        VERSION = '1.0.0'
    }

    // -----------------------
    // Build Tools (Step 11)
    // -----------------------
    tools {
        maven 'Maven'  // Name must match Jenkins Maven installation
        // Optional: configure JDK in Jenkins if needed
        // jdk 'JDK 21'
    }

    // -----------------------
    // Stages (Steps 7-9)
    // -----------------------
    stages {

        stage('Build') {
            steps {
                echo "Building project version ${VERSION}..."

                // Show Maven version
                bat 'mvn -version'

                // Only run Maven build if pom.xml exists
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
            // Conditional execution based on parameter
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

    // -----------------------
    // Post-build Actions (Steps 8 & 13)
    // -----------------------
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
