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
            withSonarQubeEnv('sonarServer') {
              sh "mvn sonar:sonar"
            }
      
           
          }
        }
         
         }

}
	 
	post {
        success {
             script {
             if (waitForQualityGate().status != "OK") {
		  slackSend (channel: '#jenkins', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: Code coverage threshold was not met! <http://192.168.1.67:9000/sonarqube/projects|Review in SonarQube>.")
             }else{ 
		  slackSend (channel: '#jenkins', color: '#29ef16', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: SUCCEFULL! <http://192.168.1.67:9000/sonarqube/projects|Review in SonarQube>.")
             }
	        }
        } 
	   unsuccessful {
	   script {
 if (waitForQualityGate().status != "OK") {
		  slackSend (channel: '#jenkins', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: Code coverage threshold was not met! <http://192.168.1.67:9000/sonarqube/projects|Review in SonarQube>.")
             }else{ 
		  slackSend (channel: '#jenkins', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: FAILLED!")
             }
	       }

        }
    }
 }
