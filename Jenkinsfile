pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh 'python3 --version'
                sh 'python3 app.py'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t jenkins-day3-docker:${BUILD_NUMBER} .'
            }
        }

    }
}