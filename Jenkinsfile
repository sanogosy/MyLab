pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
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

        // Publish the artefact on Nexus
        stage('Publish to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4.war', type: 'war']], credentialsId: '410c40c1-e8de-4f96-b33d-78dc5e076e01', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.87:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Repositories-SNAPSHOT', version: '0.0.4'
            }
        }

        stage ('Deploy'){
            steps {
                echo ' deploying......'

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