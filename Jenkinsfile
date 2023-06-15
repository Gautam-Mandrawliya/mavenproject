pipeline {
    agent any
    tools {
        maven 'Maven-Tool' 
    }

    stages {
        stage('Test') {
            steps {
                // Maven Testing
                sh 'mvn --version'
                echo 'test'
            }
        }
        stage('Build') {
            steps {
                // Maven Build
               // sh 'mvn package'
                echo 'build'
            }
        }
        stage('Deploy-On-Test') {
            steps {
                echo 'Deploying to test'
            }
        }
        stage('Deploy-On-Prod') {
            steps {
                echo 'Deploying to prod'
            }
        }
    }
    post {
        always {
            echo "It is always run!"
        }
        failure {
            echo "Failure!"
        }
        success {
            echo "Success!"
        }
    }

}
