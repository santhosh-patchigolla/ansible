pipeline {
    agent any
    environment {
        SSHCRED         = credentials('SSH_CRED')               
    }
    stages {
        stage ('') {
            steps {
                sh '''
                    ansible-playbook robot-dryrun.yaml -e COMPONENT=mongodb -e ansible_usser=centos -e ansible_password=${SSHCRED_PSW} -e ENV=dev

                ...
            }
        }
    }
}