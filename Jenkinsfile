pipeline {
    agent { label 'ansible-node' }

    environment {
        ANSIBLE_INVENTORY = /home/ubuntu/ansible/inventory.ini 
        ANSIBLE_PLAYBOOK = /home/ubuntu/ansible/nginx.yaml

    }

    stages {
        stage('checkout SCM') {
            steps {
                git branch: 'master',
                url: 'https://github.com/shankarduppala/jenkins-ansible.git'
                credentialsId: 'Git-Creds'

            }
        }

        stage('run nginx playbook on node agent') {
            steps {
                bat 'ansible-playbook -i %ANSIBLE_INVENTORY%' %ANSIBLE_PLAYBOOK%
            }
        }
    }
    post {
        success {
            echo 'deployed successfuly'
        }

        failure {
            echo 'deployment failed'
        }
    }
}