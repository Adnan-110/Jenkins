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
        stage('Terraform Create Network') {
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

        stage('Creating-EKS') {
            steps {
                dir('EKS') {  
                git branch: 'main', url: 'https://github.com/Adnan-110/Kubernetes.git'
                        sh ''' 
                            cd eks 
                            make create
                            aws eks update-kubeconfig  --name ${ENV}-eks-cluster
                            kubectl get nodes
                        ''' 
                    }
                }
            }
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
                sh "cd /home/centos/user/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
        stage('Deploying Cart') {
            steps {
                sh "cd /home/centos/cart/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
        stage('Deploying Shipping') {
            steps {
                sh "cd /home/centos/shipping/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
        stage('Deploying Payment') {
            steps {
                sh "cd /home/centos/payment/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }
        stage('Deploying Frontend') {
            steps {
                sh "cd /home/centos/frontend/"
                sh "echo Authentication To EKS"
                sh "aws eks update-kubeconfig  --name dev-eks-cluster"
                sh "kubectl get nodes"
                sh "kubectl apply -f k8-deploy.yaml"
            }
        }    
    }  
}                      