pipeline {
    agent any
    stages {
        stage('Install') {
            steps { 
                sh 'npm install' 
            }
        }

        stage('Test') {
            parallel {
                stage('Static code analysis') {
                    steps { 
                        sh 'npm run lint' 
                    }
                }
                stage('Unit tests') {
                    steps { 
                        sh 'npm run test' 
                    }
                }
            }
        }

        // stage('Build') {
        //     steps { 
        //         sh 'npm run build' 
        //     }
        // }

        // Uncomment this stage and modify as needed for your Nexus configuration
        // stage('Publish to Nexus') {
        //     steps {
        //         nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'npm-repo', packages: [[$class: 'NpmPackage', packageJson: 'package.json', path: 'dist/my-app']], protocol: 'https', repositoryName: 'my-npm-repo', serverDetails: [credentialsId: 'my-nexus-creds', nexusUrl: NEXUS_URL]
        //     }
        // }

        // stage('SonarQube analysis') {
        //     environment {
        //         // Use the SONAR_LOGIN environment variable for authentication
        //         SONAR_LOGIN = credentials('sonarqube-credentials')
        //         SONAR_HOST_URL = "http://localhost:9000"
        //     }
        //     steps {
        //         withSonarQubeEnv(credentialsId: 'sonarqube-credentials', url: SONAR_HOST_URL) {
        //             sh 'npm run sonar-scanner'
        //         }
        //     }
        // }
    }
}
