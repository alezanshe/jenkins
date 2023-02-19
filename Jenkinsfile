pipeline {
    agent any
    environment {
        VERSION = sh([ script: 'cd ./code/solution && npx -c \'echo $npm_package_version\'', returnStdout: true ]).trim()
        VERSION_RC = "rc.2"
    }
    stages {
        stage('Audit tools') {
            steps {
                sh '''
                    git version
                    docker version
                    node --version
                    npm version
                '''
            }
        }
        stage('Build') {
            steps {
                dir('./code/solution') {
                    echo "Building version ${VERSION} with suffix: ${VERSION_RC}"
                    sh '''
                        npm install
                        npm run build
                    '''
                }
            }
        }
        stage('Unit Test') {
            steps {
                dir('./code/solution') {
                    sh 'npm test'
                }
            }
        }
    }
}