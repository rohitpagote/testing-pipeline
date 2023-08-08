pipeline {
    agent any
    stages {
        stage('Checkout') {
          steps {
              checkout scmGit(
                  branches: [
                      [name: 'master']
                  ],
                  extensions: [],
                  userRemoteConfigs: [
                      [credentialsId: 'Git-Credentials', url: 'https://github.com/rohitpagote/infracost-terraform-jenkins-poc.git']
                  ]
              )
          }
        }   
        
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
