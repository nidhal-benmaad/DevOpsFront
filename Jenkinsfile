pipeline {
    agent any
    parameters {
        string(name: 'SONAR_HOST_URL', defaultValue: 'http://localhost:9000', description: 'SonarQube server URL')
        string(name: 'SONAR_USERNAME', defaultValue: '', description: 'SonarQube user login')
        string(name: 'SONAR_PASSWORD', defaultValue: '', description: 'SonarQube user password')
    }
    // environment {
    //     SONAR_URL = "http://localhost:9000"
    //     SONAR_LOGIN = credentials("sonarqube-credentials")
    // }
    // tools {
    //     nodejs 'NodeJS 18.5.0'
    // }

    stages {
        stage('Install') {
        steps { sh 'npm install' }
        }

        stage('Test') {
            parallel {
                stage('Static code analysis') {
                    steps { sh 'npm run-script lint' }
                }
                stage('Unit tests') {
                    steps { sh 'npm run-script test' }
                }
            }
        }

        stage('Build') {
        steps { sh 'npm run-script build' }
        }


        // stage('Publish to Nexus') {
        //     steps {
        //         nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'npm-repo', packages: [[$class: 'NpmPackage', packageJson: 'package.json', path: 'dist/my-app']], protocol: 'https', repositoryName: 'my-npm-repo', serverDetails: [credentialsId: 'my-nexus-creds', nexusUrl: NEXUS_URL]
        //     }
        // }
    
    }
}
