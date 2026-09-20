pipeline {
    agent any
    parameters {
        string(name: 'GREETING', defaultValue: 'Hello', description: 'Greeting message')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'staging', 'prod'], description: 'Target environment')
    }
    stages {
        stage('Greet') {
            steps {
                echo "${params.GREETING}, deploying to ${params.ENVIRONMENT}!"
            }
        }
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


        stage('Docker Build') {
            steps {
                sh 'docker build -t jenkins-demo:${BUILD_NUMBER} .'
    }
}
        stage('Docker Run Test') {
            steps {
                sh 'docker run --rm jenkins-demo:${BUILD_NUMBER}'
    }
}
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                sh 'docker tag jenkins-demo:${BUILD_NUMBER} $DOCKER_USER/jenkins-demo:${BUILD_NUMBER}'
                sh 'docker push $DOCKER_USER/jenkins-demo:${BUILD_NUMBER}'
        }
    }
}
        



        stage('Show Credential Usage') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-pat', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS')]) {
                    sh 'echo "Using credential for user: $GIT_USER"'
                }
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
