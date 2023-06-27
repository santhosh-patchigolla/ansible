pipeline {
    agent any
    environment {
        SSHCRED         = credentials('SSH_CRED')                
    }
    parameters {
        string(name: 'COMPONENT', defaultValue: 'mongodb', description: 'give the name of the component')
    }        
    stages {

        stage ('Ansible code scan') {
            steps {
                sh "echo code scan is done"
            }
        }        

        stage ('Ansible lint checks') {
            when { branch pattern: "feature-.*", comparator: "REGEXP"}
            steps {
                sh "echo lint check is done"
            }
        }        

        stage ('Ansible Dry Run') {
            when {
                branch 'prod'                               // Using this when condition we can run the Job in specific branch
            }             
            steps {
                sh ''' 
                    ansible-playbook robot-dryrun.yaml -e COMPONENT=${COMPONENT} -e ansible_user=centos -e ansible_password=${SSHCRED_PSW} -e ENV=dev
                '''       
            }
        }

        stage ('Promoting the code prod branch') {
            when {
                branch 'prod'                               // Using this when condition we can run the Job in specific branch
            }            
            steps {
                sh "echo Merging the feature branch to PROD branch"
            }
        }         
    }
}/////