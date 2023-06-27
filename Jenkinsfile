pipeline {
    agent any
    environment {
        SSHCRED         = credentials('SSH_CRED')                
    }    
    stages {
        stage ('') {
            steps {
                sh ...
                    ansible-playbook robot-dryrun.yaml -e COMPONENT=${COMPONENT} -e ansible_user=centos -e ansible_password=${SSHCRED_PSW} -e ENV=dev
                ...       
            }
        }
    }
}