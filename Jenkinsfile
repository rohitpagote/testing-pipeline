pipeline {
    agent any
    tools {nodejs "node"}
    stages {
        stage('Checkout 1') {
          steps {
              checkout scmGit(
                  branches: [
                      [name: 'master']
                  ],
                  extensions: [],
                  userRemoteConfigs: [
                      [credentialsId: 'Git-Credentials', url: 'https://github.com/rohitpagote/testing-pipeline.git']
                  ]
              )
          }
        }

        stage('Checkout external proj') {
        steps {
            // echo "checking the node version"
            // sh "npm config ls"
            // sh "npm --version"
            // sh "node --version"

            echo "${env.PIPOD_DEPLOY_INITIAL_ADMIN_USERS}"

            sh "terraform init"
            sh "terraform apply -var 'file_content=${env.PIPOD_DEPLOY_INITIAL_ADMIN_USERS}' -auto-approve"
            sh "ls"
            sh "pwd"
            sh "cat initialAdminUsers.js"
            
            // git branch: 'master',
            //     credentialsId: 'Git-Credentials',
            //     url: 'https://github.com/rohitpagote/infracost-terraform-jenkins-poc.git'

            // sh "ls -lat"
            // sh 'pwd'
            // zip zipFile: 'pipod-api-catalogs-test.zip', archive: false, dir: 'google'
            // sh 'ls'
            // sh 'pwd'
            // archiveArtifacts artifacts: 'pipod-api-catalogs-test.zip', fingerprint: true
            // sh "rm google -r"
        }
    }

        // stage('Upload zip to bucket') {
        //     // when { expression { params.action  == 'create' || params.action  == 'update' } }
        //     steps {
        //         script {
        //             echo "=== start doUpload ==="
                    
        //             withAWS(region: "us-east-1",credentials: "3a867201-f05b-49a5-9979-a057eab992af") {
        //                 s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: "pipod-api-catalogs-test.zip", bucket: "pipod-deploy-dev", path: "catalogs/")
        //             }
                    
        //             echo "=== end doUpload ==="

        //             echo "removing the zip file"
        //             sh "rm pipod-api-catalogs-test.zip"
        //         }
        //     }
        //  }

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

        // stage('Clone') {
        //     steps {
        //         sh 'git clone https://github.com/rohitpagote/infracost-terraform-jenkins-poc.git'
        //     }      
        // }
        
        // stage ('push artifact') {
        //     steps {
        //         sh 'ls'
        //         sh 'pwd'
        //         sh 'cd ..'
        //         sh 'pwd'
        //         sh 'ls'
        //         zip zipFile: 'google1.zip', archive: false, dir: 'google'
        //         sh 'ls'
        //         archiveArtifacts artifacts: 'google1.zip', fingerprint: true
        //         sh 'ls'
        //     }
        // }
    }
}
