pipeline {

    agent any
    tools {
        maven 'Maven'
    }
    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId()
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
                script {

                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "VinayDevOpsLab-SNAPSHOT" : "VinayDevOpsLab-RELEASE"

                    nexusArtifactUploader artifacts:
                    [[artifactId: "${ArtifactId}",
                    classifier: '',
                    file: "target/${ArtifactId}-${Version}.war",
                    type: 'war']],
                    credentialsId: 'e83405ae-ebc2-4dc4-b438-129f82bca9ac',
                    groupId: "${GroupId}",
                    nexusUrl: '172.20.10.61:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: "${NexusRepo}",
                    version: "${Version}"
                }
            }
         }

         //Stage 4 : Print some information
         stage('Print Environment Variables'){
            steps{
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "Group ID is '${GroupId}'"
                echo "Name is '${Name}'"
            }
         }
        //deploying stage5
        stage ('Deploy to tomcat'){
            steps{
                echo 'deploying.....'
                sshPublisher(publishers:
                [sshPublisherDesc(
                    configName: 'ansible_controller',
                    transfers: [
                        sshTransfer(
                            cleanRemote: false,
                            execCommand: 'ansible-playbook /opt/playbooks/downloadanddeploy.yaml -i /opt/playbooks/hosts',
                            execTimeout: 120000,
                    )
                ],
                usePromotionTimestamp: false,
                useWorkspaceInPromotion: false,
                verbose: false)])
            }
        }

        //deploying stage6 Deploy artifact to Docker
                stage ('Deploy to Docker'){
                    steps{
                        echo 'deploying.....'
                        sshPublisher(publishers:
                        [sshPublisherDesc(
                            configName: 'ansible_controller',
                            transfers: [
                                sshTransfer(
                                    cleanRemote: false,
                                    execCommand: 'ansible-playbook /opt/playbooks/downloadanddeploy_docker.yaml -i /opt/playbooks/hosts',
                                    execTimeout: 120000,
                            )
                        ],
                        usePromotionTimestamp: false,
                        useWorkspaceInPromotion: false,
                        verbose: false)])
                    }
                }
    }
}