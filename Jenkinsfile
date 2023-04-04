pipeline {
    agent any
    parameters {
        string(name: 'SONAR_HOST_URL', defaultValue: 'http://localhost:9000', description: 'SonarQube server URL')
        string(name: 'SONAR_LOGIN', defaultValue: '', description: 'SonarQube user login')
        string(name: 'SONAR_PASSWORD', defaultValue: '', description: 'SonarQube user password')
    }
    // environment {
    //     // Configure the Nexus repository URL and credentials
    //     NEXUS_URL = 'https://my-nexus-repo.com'
    //     NEXUS_USERNAME = credentials('my-nexus-creds').username
    //     NEXUS_PASSWORD = credentials('my-nexus-creds').password
    // }

    stages {
        stage('Build') {
            steps {
                sh 'npm --version'
                sh 'npm install'
                // sh 'npm run build --prod'
            }
        }

        // stage('SonarQube analysis') {
        //     steps {
        //         withSonarQubeEnv('My SonarQube Server') {
        //             script {
        //                 def scannerHome = tool 'SonarQube Scanner'
        //                 withEnv(["PATH+SONAR_SCANNER=${scannerHome}/bin"]) {
        //                     sh '''
        //                         sonar-scanner \
        //                             -Dsonar.host.url=${params.SONAR_HOST_URL} \
        //                             -Dsonar.login=${params.SONAR_LOGIN} \
        //                             -Dsonar.password=${params.SONAR_PASSWORD}
        //                     '''
        //                 }
        //             }
        //         }
        //     }

        // stage('Publish to Nexus') {
        //     steps {
        //         nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'npm-repo', packages: [[$class: 'NpmPackage', packageJson: 'package.json', path: 'dist/my-app']], protocol: 'https', repositoryName: 'my-npm-repo', serverDetails: [credentialsId: 'my-nexus-creds', nexusUrl: NEXUS_URL]
        //     }
        // }
    }
}
