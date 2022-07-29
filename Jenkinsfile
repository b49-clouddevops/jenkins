pipeline {
    agent any
   environment { 
        ENV_URL = 'env.pipeline.com'
        SSH_CREDS = credentials('my-predefined-username-password')
    }
    stages {
        stage('Stage one') {
            steps {
                echo "Hello world"
            }
        }

        stage('Stage two') {
            steps {
                echo "Hello Cloud"
            }
        }

        stage('Stage three') {
        environment { 
          ENV_URL = 'env.stage.com'
            }
            steps {
                sh "echo ENV_URL  =  ${ENV_URL}"
                
            }
        }
    }
}