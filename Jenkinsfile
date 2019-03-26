def qualitygate
pipeline {
  options {
    buildDiscarder logRotator(numToKeepStr: '5')
    disableConcurrentBuilds()
  }
  agent {
    kubernetes {
      cloud "go-demo-5-build"
      label "go-demo-5-build"
      serviceAccount "build"
      yamlFile "KubernetesPod.yaml"
    }      
  }
  environment {
    image = "vfarcic/go-demo-5"
    project = "go-demo-5"
  }
  stages {
    stage("build") {
                steps {
        container("maven") {
                          sh 'mvn clean package -DskipTests'
                          withSonarQubeEnv('sonarServer') {
                          sh "mvn sonar:sonar"
                                                          }
                           timeout(time: 10, unit: 'MINUTES') {

                           waitForQualityGate abortPipeline: true
                                                              }
          
          
                           }
                     }
                 }
         }
    
    
    post {
        success {
            script {
                qualitygate = waitForQualityGate().status
                if (qualitygate != "OK") {
                    slackSend(channel: '#jenkins', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: Code coverage threshold was not met! <http://sonar.192.168.1.151.nip.io |Review in SonarQube>.")
                } else {
                    slackSend(channel: '#jenkins', color: '#29ef16', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: SUCCEFULL! <http://sonar.192.168.1.151.nip.io|Review in SonarQube>.")
                }
            }
        }
        unsuccessful {
            script {
                if (qualitygate != "OK") {
                    slackSend(channel: '#jenkins', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: Code coverage threshold was not met! <http://sonar.192.168.1.151.nip.io|Review in SonarQube>.")
                } else {
                    slackSend(channel: '#jenkins', color: '#F01717', message: "*$JOB_NAME*, <$BUILD_URL|Build #$BUILD_NUMBER>: FAILLED!")
                }
            }

        }
    }
  }
