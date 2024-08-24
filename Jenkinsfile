pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Preparation') {
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

        }
        stage('Build'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Building the project"
                    chown -R 130:139 "/.npm"
                    npm install
                    npm run build
                '''
            }
        }
    }
}
