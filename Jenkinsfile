            
 pipeline {
    agent {
          any {
            sh 'echo hello k8s blue2' 
        }
    }
    stages {
        stage('Build1') { 
            steps {
                sh ' echo 11build k8S token web hook pip2' 
            }
        }
    
stage('Sonarqube') {
    environment {
        scannerHome = tool 'SonarQubeScanner'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
}
}}
