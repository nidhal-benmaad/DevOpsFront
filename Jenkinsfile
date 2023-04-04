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
    tools {
        nodejs 'NodeJS 19.8.1'
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm --version'
                sh 'npm install'
                sh 'npm run build --prod'
            }
        }

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner -Dsonar.login=${SONAR_USERNAME} -Dsonar.password=${SONAR_PASSWORD} -Dsonar.host.url=${SONAR_HOST_URL}'
                }
            }
        }


        // stage('Publish to Nexus') {
        //     steps {
        //         nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'npm-repo', packages: [[$class: 'NpmPackage', packageJson: 'package.json', path: 'dist/my-app']], protocol: 'https', repositoryName: 'my-npm-repo', serverDetails: [credentialsId: 'my-nexus-creds', nexusUrl: NEXUS_URL]
        //     }
        // }
    
    }
}
