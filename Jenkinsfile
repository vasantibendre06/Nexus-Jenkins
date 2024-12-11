pipeline {
    agent any

    environment {
        NEXUS_URL = 'http://20.127.187.253:8081'
        NEXUS_REPO = 'poc1_1'
        NEXUS_CREDENTIALS_ID = 'nexus' // Jenkins credentials ID for Nexus
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/vasantibendre06/Nexus-Jenkins.git'
            }
        }

        stage('Build Website') {
            steps {
                sh 'npm install'
                sh 'npm run build' // Adjust for your build process
            }
        }

        stage('Upload to Nexus') {
            steps {
                script {
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: "${NEXUS_URL}",
                        groupId: 'com.example',
                        version: "${BUILD_NUMBER}",
                        repository: "${NEXUS_REPO}",
                        credentialsId: "${NEXUS_CREDENTIALS_ID}",
                        artifacts: [
                            [artifactId: 'static-website', classifier: '', file: 'build.zip', type: 'zip']
                        ]
                    )
                }
            }
        }
    }
}
