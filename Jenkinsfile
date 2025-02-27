pipeline {
    agent any

    environment {
        NODE_ENV = 'development'
    }

    stages {
        stage('Setup Node.js') {
            steps {
                script {
                    def nodeInstalled = sh(script: "command -v node >/dev/null 2>&1 && echo 'yes' || echo 'no'", returnStdout: true).trim()
                    if (nodeInstalled == 'no') {
                        echo 'Node.js is not installed. Installing...'
                        sh '''
                        curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
                        apt-get install -y nodejs
                        '''
                    } else {
                        echo 'Node.js is already installed.'
                    }
                }
                sh 'node -v' // Vérification de la version installée
            }
        }

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
                // Ajoutez ici votre script de déploiement
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
