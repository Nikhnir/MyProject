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
            nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.11-snapshot.war', type: 'war']], credentialsId: 'e83405ae-ebc2-4dc4-b438-129f82bca9ac', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.61:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'NikhilDevopsLab-snapshot', version: '0.0.11-snapshot'
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