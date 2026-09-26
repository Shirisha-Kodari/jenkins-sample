
pipeline {

    // Where the Pipeline will execute
    agent {
        label 'roboshop'
    }

    // Global Pipeline configuration
    options {
        timeout(time: 1, unit: 'HOURS')
        timestamps()
    }

    // All stages must be inside ONE stages block
    stages {

        stage('Test Agent') {
            steps {
                sh 'echo "Hello from Jenkins Agent"'
                sh 'hostname'
                sh 'whoami'
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Checkout') {
            steps {
                echo 'Pulling source code from repository...'
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling the application...'
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
            when {
                branch 'main'
            }

            steps {
                echo 'Deploying application to the staging environment...'
                sh 'echo "Executing deployment scripts..."'
            }
        }
    }

    // Post-build actions
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

