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
                    sudo chown -R $USER node_modules
                    npm install -gf
                    npm i @vue/cli-service
                    npm run build
                    echo "Build completed"
                    ls -la
                '''
            }
        }
    }
}
