pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }

    stages {
        stage ('Checkout') {
            steps {
                git url: 'https://github.com/JulianMolina99/nodejs_application.git'
            }
        }
        
        stage('Build app') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        
        stage('Test app') {
            steps {
                sh 'npm test'
            }
        }
        
        stage('Analisys with sonar') {
            steps {
                script{
                    def scannerTool = tool 'SonarQube Scanner'
                    if(scannerTool){
                        withSonarQubeEnv('SonarQube Local Server'){
                            sh "${scannerTool}/bin/sonar-scanner \
                            -Dsonar.projectKey=test \
                            -Dsonar.projectName=test \
                            -Dsonar.sources=src \
                            -Dsonar.exclusions=src/__test__/** \
                            -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info"
                        }
                    } else{
                        error 'SonarQube Scanner not found'
                    }
                }
    }
}
    }
}