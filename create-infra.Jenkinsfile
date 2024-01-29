pipeline {
    agent any 
    options {
        ansiColor('xterm')
    }
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select the Environment')
        choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Select the Actionn to be Performed')
    }
    stages {
        stage('Creating VPC') {
            steps {
                dir('VPC') {
                git branch: 'main', url: 'https://github.com/Adnan-110/Terraform-vpc.git'
                        sh '''
                            terrafile -f env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                            terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                        '''
                }
            }
        }

        stage('Creating Loadbalancers') {
            steps {
                dir('ALB') {
                git branch: 'main', url: 'https://github.com/Adnan-110/Terraform-loadbalancers.git'
                        sh '''
                            terrafile -f env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                            terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                            '''
                }
            }
        }

        stage('Creating Databases') {
            steps {
                dir('DB') {
                git branch: 'main', url: 'https://github.com/Adnan-110/Terraform-databases.git'
                        sh '''
                            rm -rf .terraform
                            terrafile -f env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                            terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                        '''
                }
            }
        }
        stage('Backend') {
            parallel {
                stage('creating Catalogue') {
                    steps {
                        dir('catalogue') {   
                            git branch: 'main', url: 'https://github.com/Adnan-110/catalogue.git'
                                sh ''' 
                                    cd mutable-infra
                                    terrafile -f env-${ENV}/Terrafile
                                    terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                                    terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0
                                    terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0 -auto-approve
                                ''' 
                            }
                        }
                    } 
                stage('creating User') {
                    steps {
                        dir('user') {  git branch: 'main', url: 'https://github.com/Adnan-110/user.git'
                                sh ''' 
                                    cd mutable-infra
                                    rm -rf .terraform
                                    terrafile -f env-${ENV}/Terrafile
                                    terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                                    terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0
                                    terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0 -auto-approve
                                ''' 
                            }
                        }
                    }
                stage('creating Cart') {
                    steps {
                        dir('cart') { git branch: 'main', url: 'https://github.com/Adnan-110/cart.git'
                                sh ''' 
                                    cd mutable-infra
                                    rm -rf .terraform
                                    terrafile -f env-${ENV}/Terrafile
                                    terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                                    terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0
                                    terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0 -auto-approve
                                ''' 
                            }
                        }
                    }
                stage('creating Shipping') {
                    steps {
                        dir('shipping') { git branch: 'main', url: 'https://github.com/Adnan-110/shipping.git'
                                sh ''' 
                                    cd mutable-infra
                                    rm -rf .terraform
                                    terrafile -f env-${ENV}/Terrafile
                                    terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                                    terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0
                                    terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0 -auto-approve
                                ''' 
                            }
                        }
                    }
                stage('creating Payment') {
                    steps {
                        dir('payment') { git branch: 'main', url: 'https://github.com/Adnan-110/payment.git'
                                sh ''' 
                                    cd mutable-infra
                                    rm -rf .terraform
                                    terrafile -f env-${ENV}/Terrafile
                                    terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                                    terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0
                                    terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0 -auto-approve
                                ''' 
                                }
                        }
                    }
                }
            }
            stage('creating Frontend') {
                steps {
                    dir('frontend') {  git branch: 'main', url: 'https://github.com/Adnan-110/frontend.git'
                        sh ''' 
                            cd mutable-infra
                            rm -rf .terraform
                            terrafile -f env-${ENV}/Terrafile
                            terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0
                            terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=0.0.0 -auto-approve
                        ''' 
                    }
                }
            }
    }
        // post {
        //     always {
        //             cleanWs()
        //         }
        //     }
}


