pipeline {
    agent any
    tools {
        maven 'Maven-Tool' 
    }

    stages {
        stage('Test') {
            steps {
                // Maven Testing
                sh 'mvn test'
            }
        }
        stage('Build') {
            steps {
                // Maven Build
               sh 'mvn package'
            }
        }
        stage('Deploy-On-Test') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'Tomcat-9', path: '', url: 'http://172.31.35.175:8080')], contextPath: 'webapp', onFailure: false, war: '**/*.war'
                echo 'Deploying to test'
            }
        }
        stage('Deploy-On-Prod') {
            input {
                message 'Should we continue?'
	            ok 'Yes we continue'
                }
            steps {
                deploy adapters: [tomcat9(credentialsId: 'Tomcat-9', path: '', url: 'http://172.31.35.165:8080')], contextPath: 'webapp', onFailure: false, war: '**/*.war'
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
