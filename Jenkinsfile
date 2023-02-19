pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo "This is build number $BUILD_NUMBER" of demo $DEMO
            }
        }
    }
    environment {
        DEMO = '1'
    }
}