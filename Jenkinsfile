pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'my-react-app'  // Name of the Docker image
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the React app...'
                sh 'docker build -t $DOCKER_IMAGE:build --target build .'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'docker run --rm $DOCKER_IMAGE:build npm test'
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging the app...'
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            sh 'docker system prune -f'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
