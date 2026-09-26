pipeline {
    // Defines where the automation will execute (any available runner/agent)
    agent {
    label 'roboshop'
}
    // Optional global configurations
    options {
        timeout(time: 1, unit: 'HOURS') // Fails the build if it hangs too long
        timestamps()                    // Adds timestamps to the console logs
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling source code from repository...'
               
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling the application...'
                // Example for Linux/macOS shell. Use bat '...' for Windows.
                sh 'echo "Running build tools here (e.g., mvn clean package, npm run build)"' 
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'echo "Running test suite here (e.g., pytest, npm test)"'
            }
        }

        stage('Deploy') {
            // Evaluates a condition before running this stage
            when {
                branch 'main' // Only deploy if code is merged into the main branch
            }
            steps {
                echo 'Deploying application to the staging environment...'
                sh 'echo "Executing deployment scripts..."'
            }
        }
    }

    // Runs automatically depending on how the stages finish
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
        }
    }
}
