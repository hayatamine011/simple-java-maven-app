
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
        container("maven") {
                          sh 'mvn clean package -DskipTests'
                          withSonarQubeEnv('sonarServer') {
                          sh "mvn sonar:sonar"
                                                          }
                           timeout(time: 5, unit: 'MINUTES') {

                           waitForQualityGate abortPipeline: true
                                                              }
          
          
                   }
          }
    
    
    
  }
