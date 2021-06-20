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

        //stage3:Publish artifacts to Nexus
        stage ('Publish artifacts to Nexus'){
            steps{
            nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.11-snapshot', type: 'war']], credentialsId: '268846ff-ecf5-4fea-bb9c-304a65e858e7', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.29:8080', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://18.118.32.23:8081/repository/NikhilDevopsLab-snapshot/', version: '0.0.11-snapshot'
            }
         }
        //deploying stage4
        stage ('Deploy'){
            steps{
                echo 'deploying.....'
            }
        }
    }
}