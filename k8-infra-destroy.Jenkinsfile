pipeline {
    agent any 
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select The Environment')
        string(name: 'APP_VERSION', defaultValue: 'v01', description: 'Applicaiton Version To Be Deployed')
    }
    options {
        ansiColor('xterm')    // Add's color to the output : Ensure you install AnsiColor Plugin.
    }
    stages {
        // stage('Deleting Catalogue') {
        //     steps {
        //         dir('catalogue') {
        //         git branch: 'main', url: 'https://github.com/Adnan-110/catalogue.git'
        //         sh '''
        //             echo Authentication To EKS
        //             aws eks update-kubeconfig  --name dev-eks-cluster
        //             kubectl get nodes
        //             kubectl delete -f k8-deploy.yml
        //         '''
        //         }
        //     }
        // }
        // stage('Deleting User') {
        //     steps {
        //         dir('user') {
        //         git branch: 'main', url: 'https://github.com/Adnan-110/user.git'
        //         sh '''
        //             echo Authentication To EKS
        //             aws eks update-kubeconfig  --name dev-eks-cluster
        //             kubectl get nodes
        //             kubectl delete -f k8-deploy.yml
        //         '''
        //         }
        //     }
        // }
        // stage('Deleting Cart') {
        //     steps {
        //         dir('cart') {
        //         git branch: 'main', url: 'https://github.com/Adnan-110/cart.git'
        //         sh '''
        //             echo Authentication To EKS
        //             aws eks update-kubeconfig  --name dev-eks-cluster
        //             kubectl get nodes
        //             kubectl delete -f k8-deploy.yml
        //         '''
        //         }
        //     }
        // }
        // stage('Deploying Shipping') {
        //     steps {
        //         dir('shipping') {
        //         git branch: 'main', url: 'https://github.com/Adnan-110/shipping.git'
        //         sh '''
        //             echo Authentication To EKS
        //             aws eks update-kubeconfig  --name dev-eks-cluster
        //             kubectl get nodes
        //             kubectl delete -f k8-deploy.yml
        //         '''
        //         }
        //     }
        // }
        // stage('Deleting Payment') {
        //     steps {
        //         dir('payment') {
        //         git branch: 'main', url: 'https://github.com/Adnan-110/payment.git'
        //         sh '''
        //             echo Authentication To EKS
        //             aws eks update-kubeconfig  --name dev-eks-cluster
        //             kubectl get nodes
        //             kubectl delete -f k8-deploy.yml
        //         '''
        //         }
        //     }
        // }
        // stage('Deleting Frontend') {
        //     steps {
        //         dir('frontend') {
        //         git branch: 'main', url: 'https://github.com/Adnan-110/frontend.git'
        //         sh '''
        //             echo Authentication To EKS
        //             aws eks update-kubeconfig  --name dev-eks-cluster
        //             kubectl get nodes
        //             kubectl delete -f k8-deploy.yml
        //         '''
        //         }
        //     }
        // }
        stage('Destroying-EKS') {
            steps {
                dir('EKS') {  
                git branch: 'main', url: 'https://github.com/Adnan-110/Kubernetes.git'
                        sh ''' 
                            cd eks 
                            make destroy
                        ''' 
                    }
                }
            }
        stage('Destroying Databases') {
            steps {
                dir('DB') {
                git branch: 'main', url: 'https://github.com/Adnan-110/Terraform-databases.git'
                        sh '''
                            rm -rf .terraform
                            terrafile -f env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                            terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                        '''
                }
            }
        }
        stage('Destroying-Network') {
            steps {
                dir('VPC') { 
                git branch: 'main', url: 'https://github.com/Adnan-110/Terraform-vpc.git'
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars  -reconfigure"
                        sh "terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                    }
                }
            }
        }    
    }                        