pipeline {
    agent any
    tools {
    maven 'maven'
    }

    Stages {
        //build stage1
        stage('build'){
            steps{
                sh 'mvn clean install package'
            }
        }

        //testing stage2
        stage('test'){
            steps{
                echo 'testing...'
            }
        }

        //deploying stage3
        stage('deploy'){
            steps{
                echo 'deploying.....'
            }
        }
    }
}