node {
    def img = docker.image('gradle:jdk17')   // glibc 이미지로 고정
    img.pull()

    def cacheOpt = "-e GRADLE_USER_HOME=/home/gradle/.gradle"

    stage('prep') {
        checkout scm
        sh 'rm -rf $HOME/.gradle/native'     // 깨끗이
    }

    stage('gradle-info') {
        img.inside(cacheOpt) {
            sh 'gradle --version'
        }
    }

    stage('test') {
        img.inside(cacheOpt) {
            sh 'gradle --no-daemon test'
        }
    }

    stage('run') {
        img.inside(cacheOpt) {
            sh 'gradle --no-daemon bootRun'
        }
    }
}