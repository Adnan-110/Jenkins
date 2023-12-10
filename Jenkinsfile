// Reference : jenkins.io/doc/book/pipeline/syntax/

pipeline {
    agent any
    environment{
        ENV_URL = "pipeline.google.com"   //Global Variable

    }
    stages{
        stage('Name of the Stage - 1') {
            steps {
                sh "echo step 1"
                sh "echo step 2"
                sh "echo step 3"
            }
        }
        stage('Name of the Stage - 2') {
            environment{
                ENV_URL = "stage.google.com"  // Local Variable or Task Variable 
            }
            steps{
                    sh "echo step 1"
                    sh "echo step 2"
                    sh "echo step 3"
                }
            }
        stage('Name of the Stage - 3') {
            steps{
                sh "echo step 1"
                sh "echo step 2"
                sh "echo step 3"
            }
        }
        }
    }