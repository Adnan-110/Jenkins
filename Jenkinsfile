// Reference : jenkins.io/doc/book/pipeline/syntax/

pipeline { 
    // agent any  : This means Run on any of the available node
    agent{
        label 'ws'   //as we mentioned label as ws for one of the agent so this script will run through only that agent node
    }
    
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        // text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        // booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        // choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        // password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    environment{
        ENV_URL = "pipeline.google.com"   //Global Variable
        SSH_CRED = credentials('SSH_CRED')
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        timeout(time: 59, unit: 'MINUTES')
    }
    tools{  // This option will make build tools available only for this single run and will not install permanently.
        maven 'apache-maven-3.0.1' // This way you can directly specify the maven version from code
        maven 'maven-390' // In This way we configured in Jenkins->mangage->Tools section that whenever maven-390 is passed make maven-3.9.0 version available
    }
    triggers{
        // cron('*/1 * * * *')
        pollSCM('*/1 * * * *')
    }
    stages{
        stage('Name of the Stage - 1') {
            steps {
                sh "hostname"
                sh "mvn --version"
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