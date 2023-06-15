node {
    def dockerAgent = docker.image('node:16-buster-slim')

    stage('Checkout') {
        dockerAgent.pull()
        dockerAgent.inside() {
            checkout scm
        }
    }

    stage('Build') {
        dockerAgent.inside {
            sh 'npm install'
        }
    }

    stage('Test') {
        dockerAgent.inside {
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Manual Approval') {
        input message: "Lanjutkan ke tahap Deploy?"
    }

    stage('Deploy') {
        dockerAgent.inside {
            sh './jenkins/scripts/deliver.sh'
            sleep(time: 1, unit: 'MINUTES')
            sh './jenkins/scripts/kill.sh'   
        }
    }
}