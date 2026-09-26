
pipeline {

    // Where the Pipeline will execute
    agent {
        label 'roboshop'
    }

    environment {
        COURSE = 'jenkins'
        REGION = 'us-east-1'
    }

    // Global Pipeline configuration
    options {
        timeout(time: 30, unit: 'MINUTES') 
        timestamps()
    }

    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
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
                script {
                    sh """
                     echo "Course is: $COURSE" #  Print all environment variables
                    # env 
                    """
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit and integration tests...'

                echo "Hello: ${params.PERSON}"

                echo "Selected choice: ${params.CHOICE}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Region: ${env.REGION}"     
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

