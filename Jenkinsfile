pipeline {
    agent {
        kubernetes {
            sh 'echo hello kub' 
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
