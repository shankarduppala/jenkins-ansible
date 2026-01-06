pipeline {
    agent none  // No default agent; we will assign per stage

    environment {
        ANSIBLE_INVENTORY = '/home/ubuntu/ansible/inventory.ini'
        ANSIBLE_PLAYBOOK = '/home/ubuntu/ansible/nginx.yaml'
    }

    stages {
        stage('Checkout SCM') {
            agent { label 'windows-master' } // runs on Jenkins master (Windows)
            steps {
                git branch: 'main',
                    url: 'https://github.com/shankarduppala/jenkins-ansible.git',
                    credentialsId: 'Git-Creds'
            }
        }

        stage('Run Nginx Playbook on Linux Agent') {
            agent { label 'ansible-node' } // runs on Ubuntu agent
            steps {
                // Run Ansible on the Linux agent
                sh "ansible-playbook -i $ANSIBLE_INVENTORY $ANSIBLE_PLAYBOOK"
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
