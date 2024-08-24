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
        stage("Run tests"){
            parallel{
                stage("test1"){
                    agent {
                        docker {
                            image 'node:18-alpine'
                            args '-u root:root'
                            reuseNode true
                        }
                    }
                    steps {
                        sh '''
                            echo "Running test1"
                            
                        '''
                    }
                }
                stage("test2"){
                    agent {
                        docker {
                            image 'node:18-alpine'
                            args '-u root:root'
                            reuseNode true
                        }
                    }
                    steps {
                        sh '''
                            echo "Running test2"
                            
                        '''
                    }
                }
            }
        }
        stage("Test"){
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u root:root'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Running tests"
                    test -f 'dist/index.html'
                '''
            }
        }
        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u root:root'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install netlify-cli -g
                    netlify --version
                '''
            }
        }
    }
}
