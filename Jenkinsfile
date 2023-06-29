pipeline {
    agent any
    environment {
        SSHCRED         = credentials('SSH_CRED') 
    }
    parameters {
        string(name: 'COMPONENT', defaultValue: 'mongodb' , description: 'enter the name of the component')
    }
    stages {

        stage('Ansible Code Scan') {
            steps {
                sh  "env"
                sh  "echo Code Scan Completed"
            }
        }

        stage('Ansible Lint Checks') {
            when { branch pattern: "feature-.*", comparator: "REGEXP"}
            steps {
                sh  "env"
                sh  "echo Running aganst the feature branch whose name is ${GIT_BRANCH}"
                sh  "echo Lint Checks Completed"
            }
        }

        stage('Ansible Dry Run') {
            when { branch pattern: "PR-.*", comparator: "REGEXP"}
            steps {
                sh ''' 
                    ansible-playbook robot-dryrun.yaml -e COMPONENT=${COMPONENT} -e ansible_user=centos -e ansible_password=${SSHCRED_PSW} -e ENV=dev
                ''' 
            }
        }

        stage('Promoting Code to Prod Branch') {            
            when {
                branch 'main'                               // this when conditio is used to run the stage only at that branch level onlhy
            }
            steps {
                sh "echo Merging the feature branch to PROD Branch"
            }
        }
    }
}

