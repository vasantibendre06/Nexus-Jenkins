pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/vasantibendre06/Nexus-Jenkins.git'
            }
        }

        stage('Archive Website') {
            steps {
                sh 'zip -r website.zip .'
            }
        }

        stage('Upload to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'website',
                                                   file: 'website.zip',
                                                   type: 'zip']],
                                      credentialsId: 'nexusCredential',
                                      groupId: 'com.example',
                                      nexusUrl: 'http://18.222.76.81:8081/#admin/repository/repositories:Nexus-Jenkins',
                                      repository: 'Nexus-Jenkins',
                                      version: '1.0'
            }
        }
    }
}
