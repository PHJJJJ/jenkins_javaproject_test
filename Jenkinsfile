node {
  def myGradleContainer = docker.image('gradle:jdk17-alpine')
  myGradleContainer.pull()
  stage('prep') {
    checkout scm
  }
  stage('test') {
     myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
       sh 'gradle test'
     }
  }
  stage('run') {
     myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
       sh 'gradle bootRun'
     }
  }
}