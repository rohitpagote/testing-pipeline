pipeline {
    agent any
    stages {
        stage('Checkout 1') {
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

        //  stage('Checkout 2') {
        //      steps {
        //          checkout([
        //             $class: 'GitSCM',
        //             branches: scm.branches,
        //             extensions: scm.extensions + [[$class: 'LocalBranch'], [$class: 'WipeWorkspace']],
        //             userRemoteConfigs: [[credentialsId: 'Git-Credentials', url: 'https://github.com/rohitpagote/infracost-terraform-jenkins-poc.git']],
        //             doGenerateSubmoduleConfigurations: false
        //         ])
        //      }
        // }

        stage('Clone) {
            steps {
                sh 'git clone https://github.com/rohitpagote/infracost-terraform-jenkins-poc.git'
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
