pipeline {
    agent any
    stages {
        stage ('push artifact') {
            steps {
                sh 'ls'
                sh 'pwd'
                sh 'cd ..'
                sh 'pwd'
                sh 'ls'
                zip zipFile: 'google1.zip', archive: false, dir: 'google'
                sh 'ls'
                archiveArtifacts artifacts: 'google1.zip', fingerprint: true
                sh 'ls'
            }
        }
    }
}
