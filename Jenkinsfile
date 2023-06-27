pipeline {
    agent any
    environment {
        SSHCRED         = credentials('SSH_CRED')                
    }
    parameters {
        string(name: 'COMPONENT', defaultValue: 'mongodb', description: 'give the name of the component')
    }        
    stages {
        stage ('Ansible Dry Run') {
            steps {
                sh ''' 
                    ansible-playbook robot-dryrun.yaml -e COMPONENT=${COMPONENT} -e ansible_user=centos -e ansible_password=${SSHCRED_PSW} -e ENV=dev
                '''       
            }
        }
    }
}