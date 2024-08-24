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
                    m -rf node_modules && npm cache clean --force
                    rm -rf package-lock.json
                    npm install -g npm
                    npm ci
                    npm run build
                    echo "Build completed"
                    ls -la
                '''
            }
        }
    }
}
