import java.text.SimpleDateFormat

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
    domain = "34.210.146.155.nip.io"
    cmAddr = "cm.34.210.146.155.nip.io"
  }
  stages {
    stage("build") {
      steps {
        container("golang") {
          script {
            currentBuild.displayName = new SimpleDateFormat("yy.MM.dd").format(new Date()) + "-${env.BUILD_NUMBER}"
          }
        echo  'hello go'
        }
        container("docker") {
          echo 'hello doc'
        }
      }
    }
    
    }
  }
