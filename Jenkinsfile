node {
    def img = docker.image('gradle:jdk17')
    img.pull()

    def cacheOpt = "-e GRADLE_USER_HOME=/home/gradle/.gradle"

    stage('prep') {
        checkout scm
        sh 'rm -rf $HOME/.gradle/native'     // 클린
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
            sh 'gradle --no-daemon build'  // bootRun 대신 build 사용
        }
    }
}