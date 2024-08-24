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
                    ls -la
                    echo 'Building'
                    npm --version
                    chown -R $(whoami) ~/.npm
                    sudo npm install -g npm
                    sudo npm ci
                    npm run build
                    echo "Build completed"
                    ls -la
                '''
            }
        }
    }
}
