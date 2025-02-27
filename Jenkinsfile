pipeline {
    agent {
        docker {
            image 'node:18'  // Utilisation d'une image Node.js officielle
        }
    }

    environment {
        NODE_ENV = 'development'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js dependencies...'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'npm test'
            }
        }

        stage('Build Project') {
            steps {
                echo 'Building the project...'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
            slackSend (channel: '#ci-cd', message: "✅ Pipeline réussi : ${env.JOB_NAME} #${env.BUILD_NUMBER}")
        }
        failure {
            echo 'Pipeline execution failed!'
            slackSend (channel: '#ci-cd', message: "❌ Échec du pipeline : ${env.JOB_NAME} #${env.BUILD_NUMBER}")
        }
    }
}
