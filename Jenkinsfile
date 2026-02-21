pipeline {
    agent any

    environment {
        SSH_CRED   = 'wordpress-app-key'
        SERVER_IP  = '172.31.19.16'
        REMOTE_USER = 'ubuntu'
        APP_DIR    = '/home/ubuntu/wordpress'
    }

    stages {

        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy.git', branch: 'main'
            }
        }

        stage('Deploy WordPress with Docker') {
            steps {
                sshagent(credentials: ["${SSH_CRED}"]) {
                    sh '''
                        echo "Preparing directory on server..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "
                            mkdir -p ${APP_DIR}
                        "

                        echo "Copying docker-compose.yml to server..."
                        scp docker-compose.yml ${REMOTE_USER}@${SERVER_IP}:${APP_DIR}/

                        echo "Starting containers..."
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${SERVER_IP} "
                            cd ${APP_DIR} &&
                            docker compose down || true &&
                            docker compose up -d
                        "
                    '''
                }
            }
        }
    }
}