pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Build'){
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u root:root'
                    reuseNode true

                }
            }
            steps {
                sh '''
                    echo "Checking node version"
                    node --version
                    npm --version
                    
                '''
                sh '''
                    echo "Building the project"
                    rm -r node_modules
                    npm install
                    npm run build
                '''
            }
        }
    }
}
