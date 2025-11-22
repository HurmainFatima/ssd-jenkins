pipeline {
    agent any

    // Define parameters for conditional execution
    parameters {
        booleanParam(
            name: 'executeTests',
            defaultValue: true,
            description: 'Check to run the Test stage'
        )
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building project...'
            }
        }

        stage('Test') {
            // Conditional execution
            when {
                expression { params.executeTests == true }
            }
            steps {
                echo 'Running tests (conditional)...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying project...'
            }
        }
    }

    // Post-build actions
    post {
        always {
            echo 'Pipeline Completed'
        }
        success {
            echo 'Build Succeeded'
        }
        failure {
            echo 'Build Failed'
        }
    }
}
