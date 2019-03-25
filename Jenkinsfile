import java.text.SimpleDateFormat

<<<<<<< HEAD
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
            sh 'echo $currentBuild.displayName'
          }
        sh  'echo  k8sBuildGolang("go-demo")'
        }
        container("docker") {
          sh 'echo k8sBuildImageBeta(image, false)'
        }
      }
    }
    stage("func-test") {
      steps {
        container("helm") {
          sh 'echo k8sUpgradeBeta(project, domain, "--set replicaCount=2 --set dbReplicaCount=1")'
        }
        container("kubectl") {
        sh 'echo  k8sRolloutBeta(project)'æ
        }
        container("golang") {
          sh 'echo k8sFuncTestGolang(project, domain)'
        }
      }
      post {
        always {
          container("helm") {
            sh 'echo k8sDeleteBeta(project)'
          }
        }
      }
    }
    stage("release") {
      when {
          branch "master"
      }
      steps {
        container("docker") {
          sh 'echo k8sPushImage(image, false)'
        }
        container("helm") {
        sh 'echo  k8sPushHelm(project, "", cmAddr, true, true)'
        }
      }
    }
  }
=======

        
        }
              stage('SonarQube analysis') {
           
                withSonarQubeEnv('sonarServer') {
                    sh "mvn sonar:sonar"
                }
                timeout(time: 5, unit: 'MINUTES') {

                    waitForQualityGate abortPipeline: true
                }

           
        }
        } 
    } 
>>>>>>> a59155e8ef7392e1c86dbe349d2f36d44280dff7
}
