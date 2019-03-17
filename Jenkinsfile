pipeline {
    agent {
        kubernetes {
            sh 'echo hello k8s' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh ' echo build k8S' 
            }
        }
    }
}
