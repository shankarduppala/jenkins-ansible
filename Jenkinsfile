pipeline {
    agent { label 'ansible-node' }

    environment {
        ANSIBLE_INVENTORY: /home/ubuntu/ansible/invintory.ini 
        ANSIBLE_PLAYBOOK: /home/ubuntu/ansible/nginx.yaml

    }

    stages {
        stage('checkout SCM') {
            steps {
                git branch: 'main',
                url: 

            }
        }

        stage('run nginx playbook on node agent') {
            steps {
                sh 'ansible-playbook -i %ANSIBLE_INVENTORY%' %ANSIBLE_PLAYBOOK%
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