pipeline {
    agent any

    tools {
        nodejs 'NodeJS-24'
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh '''
                    ls -la
                    node --version
                    npm --version
                    ls -la
                '''
            }
        }
    }
}