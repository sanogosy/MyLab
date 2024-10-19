pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId()
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // stage 3 : publish artefact to Nexus
        stage ('Publish to Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: '3fa0dbd2-2464-4c55-9125-b9e96a701f24', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.67:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'VinaysDevOpsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
            }
        }

        // stage 4 : print some information
        stage('Print Environment variables'){
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID ID is '${GroupId}'"
                echo "Name is '${Name}'"
            }
        }

        // Stage3 : Deploying
        stage ('Deploy'){
            steps {
                echo 'deploying ...'
            }
        }

        // Stage3 : Publish the source code to Sonarqube
        // stage ('Sonarqube Analysis'){
        //     steps {
        //         echo ' Source code published to Sonarqube for SCA......'
        //         withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
        //              sh 'mvn sonar:sonar'
        //         }

        //     }
        // }
        
    }

}