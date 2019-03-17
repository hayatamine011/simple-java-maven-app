pipeline {
    agent {
        kubernetes {
            sh 'echo hello' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh ' echo build' 
            }
        }
    }
}
