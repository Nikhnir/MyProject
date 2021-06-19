pipeline {

    agent any
    tools {
        maven 'Maven'
    }

    stages {
        //build stage1
        stage ('Build'){
            steps{
                sh 'mvn clean install package'
            }
        }

        //testing stage2
        stage ('Test'){
            steps{
                echo 'testing...'
            }
        }

        //deploying stage3
        stage ('Deploy'){
            steps{
                echo 'deploying.....'
            }
        }
    }
}