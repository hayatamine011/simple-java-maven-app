            
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
                        sayHello 'Pinehead'
                withSonarQubeEnv('sonarServer') {
                    // Optionally use a Maven environment you've configured already
                        sh 'mvn clean package sonar:sonar'
                    
                }
                     
            
        } }
        /*stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    // Requires SonarQube Scanner for Jenkins 2.7+
                    waitForQualityGate abortPipeline: true
                }
            }
        
    
}*/
              }

                post {
        always {
	    /* Use slackNotifier.groovy from shared library and provide current build result as parameter */   
            slackNotifier(currentBuild.currentResult)
  
        }
    }
 }
       
