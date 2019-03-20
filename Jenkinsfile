 pipeline {
     agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
     
	 
stages {
     stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarServer') {
                    // Optionally use a Maven environment you've configured already
                        sh 'mvn clean package sonar:sonar'
                    
                }
	    }
         }
        stage("Quality Gate") {
            steps {

                timeout(time: 10, unit: 'MINUTES') {
              //  slackSend (channel: '#jenkins', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: Code coverage threshold was not met! <http://192.168.1.67:9000/sonarqube/projects|Review in SonarQube>.")
           
                    waitForQualityGate abortPipeline: true
                }
            }
        
          }
      }
	 
	post {
        always {
                        slack(currentBuild.currentResult)
            
        }
    }
 }
