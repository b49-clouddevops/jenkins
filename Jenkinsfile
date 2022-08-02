// pipeline {
//     agent any
//     // parameters {
//     //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
//     //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
//     //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
//     //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
//     //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
//     // }
//     environment { 
//         ENV_URL = 'env.pipeline.com'
//         SSH_CRED = credentials('SSH-Cenos7')
//     }

//     triggers { 
//          cron('0 11 * * *') 
//     }

//     tools {
//         maven 'maven-3.8.5' 
//     }

//     stages {
//         stage('Stage One') {
//         environment { 
//           ENV_URL = 'env.stage.com'
//             }
//             steps {
//                 sh "echo ENV_URL  =  ${ENV_URL}"
//                 sh "env"
//                 sh "mvn --version"              
//             }
//         }

//         stage('Two') {
//             // when { environment name: 'CHOICE', value: 'One' }
//             when {
//                 branch 'main'
//             }
//             steps {
//                 sh "echo This Stage is executed as this Choice is ONE"
//             }
//         }
        
//         // stage('Two') {
//         //     input {
//         //         message "Are you sure, you would like to contine? If yes, did you check your DevOps Lead"
//         //         ok "Yes, we should."
//         //         submitter "alice,bob"  
//         //         parameters {
//         //             string(name: 'PERSON', defaultValue: 'DevOpsLead', description: 'Ensure you check with DevOps Lead?')
//         //         }
//         //       }
//         //         steps {
//         //             sh "echo Running the statge"
//         //         }
//         //     }
//         }
//     }

pipeline {
    agent { label 'java' } 
    stages {
        stage('Parallel Stages') {
            parallel {
            stage('One') {
                steps {
                    sh "sleep 3"
                    sh "curl ifconfig.co"
                }
            }
            stage('Two') {
                steps {
                    sh "sleep 4"
                }
            }
            stage('Three') {
                steps {
                    sh "sleep 5"
                }
            }
        }
    }
        stage('Four') {
            steps {
                sh "sleep 1"
            }
        }
        stage('Sowmya') {
            steps {
                sh "sleep 1"
            }
        }
    }
post {
    aborted {
        sh "echo Job was aborted"
    }

    success {
        sh "echo Job Completed Successfully"
    }

    failure {
       cleanWs()
    }
  }
}