// Jenkinsfile - This file defines your pipeline's steps

pipeline {
    // 'agent' defines where your pipeline will run.
    // 'any' means it can run on any available Jenkins agent or the master itself.
    // For real projects, you'd specify a label like 'agent { label 'my-linux-agent' }'
    agent any

    // 'triggers' define how the pipeline starts.
    // 'pollSCM('')' is often used with webhooks. The webhook sends a notification,
    // and this trigger tells Jenkins to check for SCM changes (like your push).
    triggers {
        pollSCM('')
    }

    // 'stages' define the main phases of your pipeline.
    // Each 'stage' should represent a logical step (e.g., build, test, deploy).
    stages {
        stage('Checkout Code from Git') {
            steps {
                echo "Starting to checkout code from Git..."
                // 'checkout scm' uses the Git repository configuration you set up
                // in the Jenkins job itself. It will pull the 'develop' branch
                // because we will configure the job to only monitor that branch.
                checkout scm
                echo "Code successfully checked out into the workspace."
                // 'pwd()' prints the current working directory, useful for debugging
                echo "Current directory: ${pwd()}"
            }
        }

        stage('Verify Files') {
            steps {
                echo "Listing files to confirm checkout..."
                // 'sh' executes shell commands (for Linux/macOS agents)
                // 'bat' executes batch commands (for Windows agents)
                // We use 'isUnix()' to check the agent's OS.
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

        // You can add more stages here, for example:
        // stage('Run Tests') {
        //     steps {
        //         echo "Running unit tests..."
        //         // Example: sh 'npm test' or sh 'mvn test'
        //     }
        // }
        // stage('Build Application') {
        //     steps {
        //         echo "Building the application..."
        //         // Example: sh 'npm run build' or sh 'mvn package'
        //     }
        // }
    }

    // 'post' actions run after all stages, based on the pipeline's status.
    post {
        always {
            // 'cleanWs()' cleans up the workspace directory on the agent after the build.
            // This frees up disk space and ensures a clean state for the next build.
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
