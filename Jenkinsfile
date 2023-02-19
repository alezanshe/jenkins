pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo "This is build number $BUILD_NUMBER"
            }
        }
    }
    environment {
        DEMO = '1'
    }
}