pipeline {
    agent any

    tools {
        jdk 'jdk11'
        maven 'maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning project from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building project using Maven...'
                sh 'mvn clean package -B'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test -B'
            }
        }
    }

    post {
        always {
            echo 'Archiving test reports...'
            junit '**/target/surefire-reports/*.xml'
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
