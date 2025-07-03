pipeline {
    agent any

    environment {
        PYTHON = 'python'  // or 'python3' depending on your system
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup') {
            steps {
                bat """
                ${env.PYTHON} --version
                ${env.PYTHON} -m pip install --upgrade pip
                ${env.PYTHON} -m pip install -r requirements.txt
                """
            }
        }

        stage('Test') {
            steps {
                bat """
                ${env.PYTHON} -m pytest tests/
                """
            }
        }

        stage('Done') {
            steps {
                echo '✅ Tests passed.'
            }
        }
    }

    post {
        failure {
            echo '❌ Build failed.'
        }
    }
}
