pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello, Jenkins!'
            }
        }
        stage('Environment Info') {
            steps {
                sh 'whoami'
                sh 'pwd'
                sh 'date'
            }
        }
        stage('Create and Read File') {
            steps {
                sh 'echo "build ran at $(date)" > build-log.txt'
                sh 'cat build-log.txt'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
        always {
            echo 'This runs no matter what.'
        }
    }
}
