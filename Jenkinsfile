pipeline {
    // Run this pipeline on any available agent/worker node
    agent any 

    options {
        // Automatically fail subsequent stages if a previous stage becomes unstable
        skipStagesAfterUnstable() 
        // Timeout the entire pipeline run after 1 hour to prevent hung builds
        timeout(time: 1, unit: 'HOURS') 
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Fetching source code from repository...'
                // If using 'Pipeline script from SCM', Jenkins handles this automatically
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling the application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit and integration tests...'
                // sh 'mvn test'
                sh 'sleep 3'
            }
        }

        stage('Deploy') {
            // Optional condition: Only deploy if running on the main branch
            steps {
                echo 'Deploying application to the production server...'
                // sh './deploy.sh'
            }
        }
    }

    // Post-actions execute depending on the build outcome
    post {
        always {
            echo 'Cleaning up the workspace...'
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Sending alerts...'
            // slackSend channel: '#ci-alerts', message: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
    }
}
