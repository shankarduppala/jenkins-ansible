pipeline {
    agent { label 'ansible-node' }   // Linux Ubuntu agent

    environment {
        ANSIBLE_INVENTORY = '/home/ubuntu/ansible/inventory.ini'
        ANSIBLE_PLAYBOOK = '/home/ubuntu/ansible/nginx.yaml'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shankarduppala/jenkins-ansible.git',
                    credentialsId: 'Git-Creds'
            }
        }

        stage('Run Nginx Playbook') {
            steps {
                sh "ansible-playbook -i $ANSIBLE_INVENTORY $ANSIBLE_PLAYBOOK"
            }
        }
    }

    post {
        success {
            echo '✅ Deployment completed successfully'
        }
        failure {
            echo '❌ Deployment failed'
        }
    }
}
