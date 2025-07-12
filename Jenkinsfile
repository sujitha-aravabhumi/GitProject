pipeline {
    
    agent any
    triggers {
        pollSCM('')
    }

    stages {
        stage('Checkout Code from Git') {
            steps {
                echo "Starting to checkout code from Git..."
                checkout scm
                echo "Code successfully checked out into the workspace."
                echo "Current directory: ${pwd()}"
            }
        }

        stage('Verify Files') {
            steps {
                echo "Listing files to confirm checkout..."
                script {
                    if (isUnix()) {
                        sh 'ls -la' // List all files and directories
                    } else {
                        bat 'dir /b /s' // List files and directories
                    }
                }
                echo "File listing complete."
            }
        }

    }

    post {
        always {
            cleanWs()
            echo "Pipeline finished. Workspace cleaned."
        }
        success {
            echo "Pipeline completed successfully! :)"
        }
        failure {
            echo "Pipeline failed! :("
        }
    }
}
