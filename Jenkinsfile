pipeline {
    agent any
   environment { 
        ENV_URL = 'env.pipeline.com'
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
            steps {
                sh "echo ENCV"
                
            }
        }
    }
}