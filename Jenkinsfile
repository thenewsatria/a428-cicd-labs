node {
    def dockerAgent = docker.image('node:16-buster-slim')

    stage('Checkout') {
        dockerAgent.pull()
        dockerAgent.inside("-p 3000:3000") {
            checkout scm
        }
    }

    stage('Build') {
        dockerAgent.inside("-p 3000:3000") {
            sh 'npm install'
        }
    }

    stage('Test') {
        sh './jenkins/scripts/test.sh'
    }
}