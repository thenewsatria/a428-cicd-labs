node {
    def dockerAgent = docker.image('node:16-buster-slim')

    stage('Checkout') {
        dockerAgent.pull()
        dockerAgent.withRun("-p 3000:3000") {
            checkout scm
        }
    }

    stage('Build') {
        dockerAgent.withRun("-p 3000:3000") {
            sh 'npm install'
        }
    }

    stage('Test') {
        dockerAgent.withRun("-p 3000:3000") {
            sh './jenkins/scripts/test.sh'
        }
    }
}