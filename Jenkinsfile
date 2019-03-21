 
def qualitygate
pipeline {
     agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
     
	 
stages {
     stage('build ') {
	      steps {
                    // Optionally use a Maven environment you've configured already
                        sh 'mvn clean package -DskipTests'
                    
                
	      }}
	      stage('SonarQube analysis') {
	             steps {
          script {
            STAGE_NAME = "SonarQube analysis"
      
            withSonarQubeEnv('sonarServer') {
              sh "mvn sonar:sonar"
            }
      
           
          }
        }
           /* steps {
                withSonarQubeEnv('sonarServer') {
                    // Optionally use a Maven environment you've configured already
                        sh 'mvn clean package sonar:sonar'
                    
                }
	    }*/
         }
        stage("Quality Gate") {
		
        steps {
             script {
            qualitygate = waitForQualityGate()
            echo qualitygate.status
            if (qualitygate.status != "OK") {
              currentBuild.result = "FAILURE"
		    slack('FAILURE')
              //slackSend (channel: '#jenkins', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: Code coverage threshold was not met! <http://****.com:9000/sonarqube/projects|Review in SonarQube>.")
            }
              
            }
	          }
          }
      }
	 
	post {
        always {script {
            
            //if (qualitygate.status != "OK") {
              //currentBuild.result = "FAILURE"
		    slack('FAILURE')
              //slackSend (channel: '#jenkins', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: Code coverage threshold was not met! <http://****.com:9000/sonarqube/projects|Review in SonarQube>.")
	    //}
	       }
             //slack(currentBuild.currentResult)
            
        }
    }
 }
