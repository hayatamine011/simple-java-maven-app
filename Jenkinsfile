            
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

                     
            
        } }
             
              
        
             }

                post {
        always {
	    /* Use slackNotifier.groovy from shared library and provide current build result as parameter */   
		slackNotifier 'SUCCESS'
		 echo "Pipeline result: ${currentBuild.result}"
		            echo "Pipeline currentResult: ${currentBuild.currentResult}"

  
        }
    }
 }
       
