pipeline{
    agent{
        docker{
            image "node:lts-jod"
            args "-u root"
        }
    }
  stages{
    stage("Installing"){
      steps{
        sh "npm install"
      }
    }
  }
}
