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
                echo 'Building..'
                '''
                echo 'Building..'
                npm install
                npm run build
                '''
            }
        }
    }
}
