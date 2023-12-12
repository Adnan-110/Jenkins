// Reference : jenkins.io/doc/book/pipeline/syntax/

pipeline {
    agent any
    environment{
        ENV_URL = "pipeline.google.com"   //Global Variable
        SSH_CRED = credentials('SSH_CRED')
        // password = credentials('PASSWORD')

    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    stages{
        stage('Name of the Stage - 1') {
            steps {
                sh "echo Hello World"
                sh "echo Name of the Variable is ${ENV_URL}"
                sh "env"
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