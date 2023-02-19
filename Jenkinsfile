pipeline {
    agent any
    /*diff*/
    parameters {
        booleanParam(name: 'RC', defaultValue: false, description: 'Is this a Release Candidate?')
    }
    /*diff*/
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
            /*diff*/
            environment {
                VERSION_SUFFIX = sh(script:'if [ "${RC}" == "true" ] ; then echo -n "${VERSION_RC}+ci.${BUILD_NUMBER}"; else echo -n "${VERSION_RC}"; fi', returnStdout: true)
            }
            /*diff*/
            steps {
                dir('./code/solution') {
                    // echo "Building version ${VERSION} with suffix: ${VERSION_RC}"
                    echo "Building version ${VERSION} with suffix: ${VERSION_SUFFIX}"
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
        /*diff*/
        stage('Publish') {
            when {
                expression { return params.RC }
            }
            steps {
                archiveArtifacts('01/solution/app/')
            }
        }
        /*diff*/
    }
}