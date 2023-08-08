pipeline {
    agent any
    stages {
        stage ('push artifact') {
            steps {
                sh 'ls'
                sh 'pwd'
                sh 'mkdir archive'
                sh 'ls'
                sh 'echo test > archive/test.txt'
                sh 'ls'
                zip zipFile: 'test.zip', archive: false, dir: 'archive'
                sh 'ls'
                archiveArtifacts artifacts: 'test.zip', fingerprint: true
                sh 'ls'
            }
        }
    }
}
