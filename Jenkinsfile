// Reference : jenkins.io/doc/book/pipeline/syntax/

pipeline {
    agent any
    environment{
        ENV_URL = "pipeline.google.com"   //Global Variable

    }
    stages{
        stage('Name of the Stage - 1') {
            steps {
                sh "echo Hello"
                sh "echo World"
                sh "echo Name of the Variable is ${ENV_URL}"
            }
        }
        stage('Name of the Stage - 2') {
            environment{
                ENV_URL = "stage.google.com"  // Local Variable or Task Variable 
            }
            steps{
                    sh "echo Name of the Varible is ${ENV_URL}"
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