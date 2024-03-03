pipeline {
    agent any 
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select The Environment')
    }
    options {
        ansiColor('xterm')    // Add's color to the output : Ensure you install AnsiColor Plugin.
    }
    stages {
        stage('Deploying Catalogue') {
            steps {
                sh "cd /home/centos/catalogue/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
        stage('Deploying User') {
            steps {
                sh "/home/centos/user/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
        stage('Deploying Cart') {
            steps {
                sh "/home/centos/cart/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
        stage('Deploying Shipping') {
            steps {
                sh "/home/centos/shipping/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
        stage('Deploying Payment') {
            steps {
                sh "/home/centos/payment/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
        stage('Deploying Frontend') {
            steps {
                sh "/home/centos/frontend/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
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