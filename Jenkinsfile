pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {

        stage('Init POM variables') {
            steps {
                script {
                    def pom = readMavenPom file: 'pom.xml'
                    env.ArtifactId = pom.artifactId
                    env.Version    = pom.version
                    env.GroupId    = pom.groupId
                    env.Name       = pom.name
                }
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install package'
            }
        }

        stage('Test') {
            steps {
                echo 'testing...'
            }
        }

        stage('Publish to Nexus') {
            steps {
                script {
                    def NexusRepo = env.Version.endsWith("SNAPSHOT") ? "Repositories-SNAPSHOT" : "Repositories-RELEASE"

                    nexusArtifactUploader artifacts: [[
                        artifactId: env.ArtifactId,
                        classifier: '',
                        file: "target/${env.ArtifactId}-${env.Version}.war",
                        type: 'war'
                    ]],
                    credentialsId: '410c40c1-e8de-4f96-b33d-78dc5e076e01',
                    groupId: env.GroupId,
                    nexusUrl: '172.20.10.87:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: NexusRepo,
                    version: env.Version
                }
            }
        }

        stage('Print Environment variables') {
            steps {
                echo "Artifact ID: ${env.ArtifactId}"
                echo "Version: ${env.Version}"
                echo "GroupId: ${env.GroupId}"
                echo "Name: ${env.Name}"
            }
        }

        stage('Deploy') {
            steps {
                echo 'deploying...'
            }
        }
    }
}