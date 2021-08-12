pipeline {

  //node ('JenkinsSlave')
  agent { label 'JenkinsSlave' }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/snadimpally/hellowhale.git', branch:'master'
      }
    }
    
      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("4599/hellowhale:${env.BUILD_ID}")
                }
            }
        }
    
      stage('Publish Docker Image'){
            steps {
                script {
                    myapp = docker.build("4599/hellowhale:${env.BUILD_ID}")
                }
            }
         withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerPWD')]) {
              sh "docker login -u intdoc89 -p ${dockerPWD}"
         }
        sh "docker push ${myapp}"
        
      }
        }

    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "hellowhale.yml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
