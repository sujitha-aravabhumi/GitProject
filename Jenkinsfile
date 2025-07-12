pipeline {
    
    agent any
    triggers {
        pollSCM('')
    }

    stages {
        stage('Checkout Code to specific folder') {
            steps {
                def targetRepoFolder = "pulled-code"
                echo "Attempting to checkout code into: ${targetRepoFolder}"
                dir(targetRepoFolder){
                    checkout scm
                echo "Code successfully checked out into: ${pwd()}"
                }
                echo "checkout operation completed."
                }
            }
        }

        stage('Verify content in Folder') {
            steps {
                echo "Listing files to confirm checkout..."
                script {
                    def sourcecodeLocation = "pulled-code"
                    echo "source_code_location: ${sourcecodeLocation}"
                    if (isUnix()){
                         sh 'ls -la'
                    }else{
                        bat 'dir /b /s'
                    }
                }
                echo "Content verification complete."
            }
        }

    post {
        always {
            cleanWs()
            echo "Pipeline finished. Workspace cleaned."
        }
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}

