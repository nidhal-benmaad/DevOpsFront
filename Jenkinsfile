pipeline {
    agent any
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "localhost:8081"
        NEXUS_REPOSITORY = "AngularAppRepo"
        NEXUS_CREDENTIAL_ID = "nexus-credentials"

        DOCKERHUB_CREDENTIALS = credentials('docker-credentials')
    }
    stages {
        stage('Install') {
            steps { 
                sh 'npm install' 
            }
        }

        // stage('Test') {
        //     parallel {
        //         stage('Static code analysis') {
        //             steps { 
        //                 sh 'npm run lint' 
        //             }
        //         }
        //         stage('Unit tests') {
        //             steps { 
        //                 sh 'npm run test' 
        //             }
        //         }
        //     }
        // }

        stage('Build') {
            steps { 
                sh 'npm run build' 
            }
        }

           stage('Package') {
            steps {
                sh 'zip -r angular-app.zip dist'
            }
        }
        stage('Upload to Nexus') {
            steps {
                 // sh 'cd dist && npm publish --registry=http://your-nexus-repository-url/repository/your-nexus-repository-name/ --access=public'
                nexusArtifactUploader(
                    nexusVersion: NEXUS_VERSION,
                    protocol: 'http',
                    nexusUrl: NEXUS_URL,
                    groupId: 'com.example',
                    artifactId: 'my-angular-app',
                    version: '1.0',
                    packaging: 'zip',
                    repository: NEXUS_REPOSITORY,
                    credentialsId: NEXUS_CREDENTIAL_ID,
                    file: 'angular-app.zip'
                )
            }
        }
    }
}
