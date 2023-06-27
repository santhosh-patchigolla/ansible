pipeline {
    agent any
    environment {
        SSHCRED         = credentials('SSH_CRED')               
    }
    parameters {
        string(name: 'COMPONENT', defaultValue: 'mongodb', description: 'give the name of the component')
    }    
    stages {

        stage ('Ansible dry-run') {
            steps {
                sh '''
                    ansible-playbook robot-dryrun.yaml -e COMPONENT=mongodb -e ansible_usser=centos -e ansible_password=${SSHCRED_PSW} -e ENV=dev
                ...
            }
        }
    }
}