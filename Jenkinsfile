pipeline {
    agent any
    stages {
        stage ('push artifact') {
            steps {
                sh 'ls'
                sh 'pwd'
                zip zipFile: 'google.zip', archive: false, dir: 'google'
                sh 'ls'
                archiveArtifacts artifacts: 'google.zip', fingerprint: true
                sh 'ls'
            }
        }
    }
}
