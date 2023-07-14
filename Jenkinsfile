pipeline {
    agent any
    stages {
        stage('infracost API key'){
              steps {
                  withCredentials([
                    usernamePassword(
                        credentialsId: 'a8374e7e-b007-4497-a068-f26bc554a776', 
                        usernameVariable: 'USER', 
                        passwordVariable: 'PASS'
                        )]) {
                    sh '''
                        echo "The username is: ${USER}"
                        echo "The password is : ${PASS}"
                    '''
                }
              }
        }
        stage('infracost') {

            // Set up any required credentials for posting the comment, e.g. GitHub token, GitLab token
            environment {
                // INFRACOST_API_KEY = credentials('jenkins-infracost-api-key')
                INFRACOST_API_KEY = "${PASS}"
                // The following environment variables are required to show Jenkins PRs on Infracost Cloud.
                //  These are the minimum required, and you should alter to conform to your specific setup.
                //  To read more about additional environment variables you can use to customize Infracost Cloud,
                //  visit here: https://www.infracost.io/docs/features/environment_variables/#environment-variables-to-set-metadata
                INFRACOST_VCS_PROVIDER = 'github'
                INFRACOST_VCS_REPOSITORY_URL = 'https://github.com/rohitpagote/infracost-terraform-jenkins-poc.git'
                INFRACOST_VCS_PULL_REQUEST_URL = 'https://github.com/rohitpagote/infracost-terraform-jenkins-poc/pull/3'
                INFRACOST_VCS_PULL_REQUEST_AUTHOR = 'Rohit Pagote'
                INFRACOST_VCS_PULL_REQUEST_TITLE = 'Change instance type'
                INFRACOST_VCS_BRANCH = 'master'
                INFRACOST_VCS_BASE_BRANCH = 'master'
                INFRACOST_VCS_COMMIT_SHA = '3ab6d626f5172b205c1a068dbaf346b23bf94e20'
                // If you're using Terraform Cloud/Enterprise and have variables or private modules stored
                // on there, specify the following to automatically retrieve the variables:
                // INFRACOST_TERRAFORM_CLOUD_TOKEN: credentials('jenkins-infracost-tfc-token')
                // Change this if you're using Terraform Enterprise
                // INFRACOST_TERRAFORM_CLOUD_HOST: app.terraform.io
            }

            steps {
                // Get the infracost version
                sh 'infracost --version'
                // Clone the base branch of the pull request (e.g. main/master) into a temp directory.
                sh 'git clone https://github.com/rohitpagote/infracost-terraform-jenkins-poc.git --branch=master --single-branch /tmp/base'

                sh 'infracost breakdown --path=/tmp/base'

                // Generate Infracost JSON file as the baseline, add any required sub-directories to path, e.g. `/tmp/base/PATH/TO/TERRAFORM/CODE`.
                sh 'infracost breakdown --path=/tmp/base \
                                        --format=json \
                                        --out-file=tmp/infracost-base.json'

                // Generate an Infracost diff and save it to a JSON file.
                sh 'infracost diff --path=/tmp/base \
                                   --format=json \
                                   --compare-to=/tmp/infracost-base.json \
                                   --out-file=/tmp/infracost.json'

                // Posts a comment to the PR using the 'update' behavior.
                // This creates a single comment and updates it. The "quietest" option.
                // The other valid behaviors are:
                //   delete-and-new - Delete previous comments and create a new one.
                //   hide-and-new - Minimize previous comments and create a new one.
                //   new - Create a new cost estimate comment on every push.
                // See https://www.infracost.io/docs/features/cli_commands/#comment-on-pull-requests for other options.
                // sh 'infracost comment github --path=/tmp/infracost.json \
                //                              --repo=https://github.com/rohitpagote/infracost-terraform-jenkins-poc.git \
                //                              --pull-request=$GITHUB_PULL_REQUEST_NUMBER \
                //                              --github-token=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 \
                //                              --behavior=update'
            }
        }
    }
}
