pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Checking node and npm versions"
                    npm --version
                    node --version
                    ls -al
                '''
            }

            steps
            {
                sh '''
                echo "Building.."
                npm install
                npm run build
                '''
            }
        }
    }
}
