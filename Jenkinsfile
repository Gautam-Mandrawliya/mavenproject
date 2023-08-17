pipeline {
    agent any
    tools {
        maven 'Maven-Tool' 
    }
   // triggers {
  	//pollSCM 'H/2  *  *  *  *'
 //   }

    stages {
        stage('Test') {
            steps {
	//	slackSend channel: 'jenkinsproject', message: 'Job started!'
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
                deploy adapters: [tomcat9(credentialsId: 'Tomcat-9', path: '', url: 'http://172.31.5.144:8080')], contextPath: 'app', onFailure: false, war: '**/*.war'
                echo 'Deploying to test'
            }
        }
        stage('Deploy-On-Prod') {
            input {
                message 'Should we continue?'
	            ok 'Yes we continue'
                }
            steps {
                deploy adapters: [tomcat9(credentialsId: 'Tomcat9', path: '', url: 'http://172.31.13.24:8080')], contextPath: 'app', onFailure: false, war: '**/*.war'
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
	//    slackSend channel: 'jenkinsproject', message: 'Success!'
        }
    }

}
