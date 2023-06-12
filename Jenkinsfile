node {
    def dockerAgent = docker.image('node:16-buster-slim')

    stage('Checkout') {
        dockerAgent.pull()
        dockerAgent.withRun("-p 3000:3000").inside {
            checkout scm
        }
    }

    stage('Build') {
        dockerAgent.withRun("-p 3000:3000").inside {
            sh 'npm install'
        }
    }

    stage('Test') {
        dockerAgent.withRun("-p 3000:3000").inside {
            sh './jenkins/scripts/test.sh'
        }
    }
}