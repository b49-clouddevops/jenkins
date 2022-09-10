// Here is the order to delete the whole infra in a single shot;
// Network should be the last component all the time
pipeline {
    agent any
    parameters
         { 
            choice(name: 'ENV', choices: ['dev', 'prod'], description: 'ENV')
            string(name: 'APP_VERSION', defaultValue: '', description: 'Just give dummy value - Ignore this VPC ALB and DB')     
          }
   
    stages {
         stage('Backend-1') {
            parallel {
               stage('Deleting-User') {
                   steps {
                       dir('USER') {  git branch: 'main', url: 'https://github.com/b49-clouddevops/user.git'
                          sh '''
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                            }
                        }
                   }
               stage('Deleting-Catalogue') {
                   steps {
                       dir('Catalogue') {  git branch: 'main', url: 'https://github.com/b49-clouddevops/catalogue.git'
                          sh '''
                            sleep 40
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                            }
                        }
                  }
            stage('Deleting-Payment') {
                steps {
                    dir('PAYMENT') {  git branch: 'main', url: 'https://github.com/b49-clouddevops/payment.git'
                          sh '''
                            sleep 90
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                         }
                     }
                }
            stage('Deleting-Cart') {
                steps {
                    dir('CART') {  git branch: 'main', url: 'https://github.com/b49-clouddevops/cart.git'
                          sh '''
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                         }
                     }
                }
            stage('Deleting-Shipping') {
                steps {
                    dir('SHIPPING') {  git branch: 'main', url: 'https://github.com/b49-clouddevops/shipping.git'
                          sh '''
                            cd terraform-mutable
                            export TF_VAR_APP_VERSION=3.0.0
                            terrafile -f env-${ENV}/Terrafile
                            terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                            terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                          '''
                         }
                     }
                }
            stage('Deleting-Frontend') {
                       steps {
                           dir('FRONTEND') {  git branch: 'main', url: 'https://github.com/b49-clouddevops/frontend.git'
                              sh '''
                                pwd ; ls -ltr
                                cd ./terraform-mutable
                                export TF_VAR_APP_VERSION=3.0.0
                                terrafile -f env-${ENV}/Terrafile
                                terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                                terraform plan -var-file=env-${ENV}/${ENV}.tfvars
                                terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve
                              '''
                                }
                            }
                       }
             } // Parallel Stages Completed
          }   // Stage Completed
      stage('Deleting DB and ALB') {
      parallel {

        stage('Deleting-DB') {
            steps {
            dir('EC2') { git branch: 'main', url:'https://github.com/b49-clouddevops/terraform-databases.git'
                       sh "ls -ltr"
                       sh "export TF_VAR_APP_VERSION=3.0.0"
                       sh "terrafile -f env-${ENV}/Terrafile"
                       sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                       sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                       sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars || true"
                       sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
                    }
               }
        }
        stage('Deleting-ALB') {
            steps {
                dir('VPC') {  git branch: 'main', url: 'https://github.com/b49-clouddevops/tf-loadbalancers.git'
                        sh "ls -ltr"
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
                        }
                    }
                }
              } // Parallel Stages Completed
           }   // Stage Completed
          
        stage('Deleting-VPC') {   // Network should be the last
            steps {
                dir('VPC') {  git branch: 'main', url: 'https://github.com/b49-clouddevops/terraform-vpc.git'
                        sh "ls -ltr"
                        sh "export TF_VAR_APP_VERSION=3.0.0"
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init -backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars"
                     }
                 }
            }       
        }
    }