pipeline {
    agent any
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    environment { 
        ENV_URL = 'env.pipeline.com'
        SSH_CRED = credentials('SSH-Cenos7')
    }

    triggers { 
         cron('*/2 * * * *') 
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
                sh "env"
                
            }
        }
    }
}